# idf.py 工具

`idf.py -p COMn erash-flash`
`idf.py create-project <project name>` 创建工程
`idf.py set-target <target>` 选择目标板
`idf.py size-components` 显示大小
`idf.py reconfigure` 此命令将重新运行 [CMake](https://cmake.org/)。正常情况下并不会用到该命令，因为一般无需重新运行 CMake，但如果从源代码树中添加或删除了文件，或需要修改 CMake 缓存变量时，将有必要使用该命令。例如，`idf.py -DNAME='VALUE' reconfigure` 可将变量 `NAME` 在 CMake 缓存中设置为值 `VALUE`。 

`idf.py uf2` 此命令将在构建目录中生成一个 UF2（[USB 烧录格式](https://github.com/microsoft/uf2)) 二进制文件 `uf2.bin`，该文件包含所有烧录目标芯片所必需的二进制文件，即引导加载程序、应用程序和分区表。

# idf组件管理
IDF 组件管理器工具用于下载 ESP-IDF CMake 项目的依赖项，该下载在 CMake 运行期间自动完成。IDF 组件管理器可以从 [组件注册表](https://components.espressif.com/) 或 Git 仓库获取组件。

要获取组件列表，请参阅 [https://components.espressif.com/](https://components.espressif.com/).

有关 IDF 组件管理器的详细信息，请参阅 [IDF 组件管理器及 ESP 组件注册表文档](https://docs.espressif.com/projects/idf-component-manager/en/latest/)。

## 在项目中使用 IDF 组件管理器[](https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32/api-guides/tools/idf-component-manager.html#id1 "永久链接至标题")

项目中各组件的依赖项定义在单独的清单文件中，命名为 `idf_component.yml`，位于组件根目录。运行 `idf.py create-manifest` 可以为组件创建清单文件模板。默认情况下将为 main 组件创建清单文件。使用 `--path` 选项，可以显式指定创建清单文件的目录路径。使用 `--component=my_component` 选项可以指定组件名称，这样系统将会在 `components` 文件夹下为该组件创建清单文件。`create-manifest` 命令支持以下运行方式：

- `idf.py create-manifest` 为 main 组件创建清单文件
    
- `idf.py create-manifest --component=my_component` 在 `components` 目录下，为组件 **my_component** 创建清单文件
    
- `idf.py create-manifest --path="../../my_component"` 在 `my_component` 目录下，为组件 **my_component** 创建清单文件
    

在向项目的某个组件添加新的清单时，必须先运行 `idf.py reconfigure`，手动重新配置项目。随后，构建过程将跟踪 `idf_component.yml` 清单的变更，并在必要时自动触发 CMake。

要为 ESP-IDF 项目中的组件（如 `my_component`）添加依赖项，可以运行命令 `idf.py add-dependency DEPENDENCY`。`DEPENDENCY` 参数代表一个由 IDF 组件管理器管理的额外组件，而 `my_component` 也依赖于这个组件。`DEPENDENCY` 参数的格式为 `namespace/name=1.0.0`，namespace/name 代表组件名称，=1.0.0 是组件的版本范围，详情请参阅 [版本文档](https://docs.espressif.com/projects/idf-component-manager/en/latest/reference/versioning.html)。默认情况下，依赖项会添加到 main 组件。通过使用 `--path` 选项，可以显式指定包含清单的目录，也可以使用 `--component=my_component`，在 `components` 文件夹中指定组件。`add-dependency` 命令支持以下运行方式：

- `idf.py add-dependency example/cmp` 为 main 组件添加依赖项，依赖项为 `example/cmp` 的最新版本
    
- `idf.py add-dependency --component=my_component example/cmp<=3.3.3` 将依赖项添加到位于 `components` 目录下名为 `my_component` 的组件中，依赖项为版本号 `<=3.3.3` 的 `example/cmp`
    
- `idf.py add-dependency --path="../../my_component" example/cmp^3.3.3` 将依赖项添加到位于目录 `my_component` 下名为 `my_component` 的组件中，依赖项为版本号 `^3.3.3` 的 `example/cmp`
    

备注

`add-dependency` 命令会从 [乐鑫组件注册表](https://components.espressif.com/) 将依赖项显式添加到你的项目中。

要更新 ESP-IDF 项目的依赖项，请运行命令 `idf.py update-dependencies`。你也可以使用 `--project-dir PATH` 选项，指定项目目录的路径。

应用程序示例 [build_system/cmake/component_manager](https://github.com/espressif/esp-idf/tree/341a8f2/examples/build_system/cmake/component_manager) 使用了由组件管理器安装的组件。

对于不需要受管理依赖项的组件，则无需提供清单文件。

在 CMake 配置项目（如 `idf.py reconfigure`）时，组件管理器会执行以下操作：

- 处理项目中每个组件的 `idf_component.yml` 清单，并递归解析依赖项。
    
- 在项目根目录中创建 `dependencies.lock` 文件，包含完整的依赖项列表。
    
- 将所有依赖项下载至 `managed_components` 目录。
    

请勿更改 `dependencies.lock` 锁文件和 `managed_components` 目录的内容。组件管理器运行时，会始终确保这些文件处于最新状态。如果意外修改了这些文件，可以通过使用 `idf.py reconfigure` 触发 CMake，重新运行组件管理器。

设置构建属性 `DEPENDENCIES_LOCK` 可以指定顶层 CMakeLists.txt 文件中的锁文件路径。例如，在 `project(PROJECT_NAME)` 前添加 `idf_build_set_property(DEPENDENCIES_LOCK dependencies.lock.${IDF_TARGET})`，可以为不同目标生成不同锁文件。