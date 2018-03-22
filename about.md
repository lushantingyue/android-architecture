本项目的实现思想: 由两部分组成, 数据仓库/加载层 和 功能模块下的 M-V-P分层架构.

Part1: 数据仓库 + 加载层
=========================================

TasksLocalDataSource 持有 TasksPersistenceContract类 和 TasksDbHelper类

TasksDataSource接口类

TasksLocalDataSource 本地数据加载类
          |      (use it)
          |--- TasksPersistenceContract类
          |--- TasksDbHelper类

TasksRemoteDataSource 远端数据加载类(模拟)
          |        (use it)
          |---

TasksRepository 把本地/远端Task数据 缓存至页面
          |      (use it)
          |--- TasksLocalDataSource
          |--- TasksRemoteDataSource

TaskLoader,TasksLoader 均继承自AsyncTaskLoader, 总览异步加载过程

TaskLoader 总览异步加载过程, 用于(单个)任务详情/任务编辑页
          |        (use it)
          |--- TasksRepository

TasksLoader 总览异步加载过程, 用于(多个)任务列表/统计页
          |        (use it)
          |--- TasksRepository

数据实体类 Task

Part2: 功能模块/ M-V-P分层架构.
=========================================

本项目 M-V-P架构的实现思路:

Activity持有 TaskPresenter 和 任务标记 TasksFilterType/EXTRA_TASK_ID
TaskPresenter 持有 Fragment(TaskView) 和 TaskRepository(Model) LoaderManager(受生命周期事件支配)

在另一个项目 todo-mvp-rxjava 中, presenter层: 使用rxjava订阅 替代 loader/loaderManager

