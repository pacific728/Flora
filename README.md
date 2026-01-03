**Flora - Kotlin & Material Design 打印管理系统**
 
项目简介
 
Flora 是一款基于 Kotlin 语言开发、遵循 Material Design 3 设计规范的打印管理软件，专为 Android 11（API Level 30）及以上设备打造。软件深度集成 Android 系统打印框架（PrintManager），聚焦打印任务全流程管理、打印机设备监控与队列调度核心需求，适配系统交互规范与分区存储政策，提供简洁流畅的操作体验，适用于个人办公与小型团队场景。
 
技术栈
 
- 开发语言：Kotlin
- UI 框架：Material Design 3（原生适配 Android 11 深色模式、圆角控件规范）
- 核心技术：Android 系统打印接口（ android.print  包）
- 最低兼容版本：Android 11 (API Level 30)
- 核心依赖库
- Material Components for Android：实现 MD3 控件与主题
- AndroidX Core & Appcompat：兼容 Android 11 系统 API
- Room Database：本地打印任务数据持久化
- Coroutines + Flow：异步任务处理，规避 Context 泄漏风险
- AndroidX Activity Result API：替代  startActivityForResult ，适配 Android 11 权限机制
 
功能特性
 
1. 系统打印接口集成（核心功能）
- 调用系统  PrintManager  创建打印任务，支持 PDF、图片、文本等格式文件打印
- 自定义打印属性（纸张大小、打印方向、色彩模式、双面打印），与系统打印设置无缝对接
- 监听系统打印任务状态（待打印、打印中、已完成、失败、取消），实时同步至本地任务列表
2. 任务管理
- 查看、暂停、取消队列中的系统打印任务，支持失败任务一键重试
- 按优先级排序任务队列，高优先级任务优先调用系统打印服务
- 本地存储打印任务历史记录，支持按时间、状态筛选查询
3. 设备管理
- 调用系统打印接口获取已配对打印机列表，支持手动添加网络打印机
- 实时监控打印机状态（在线/离线/缺纸/故障），异常状态即时推送系统通知
4. 系统适配（重点功能）
- 严格遵循 Android 11 Context 使用规范，全局模块采用 Application Context，页面交互采用 Activity Context，杜绝内存泄漏
- 适配 Android 11 分区存储政策，通过系统文件选择器选取打印文件，无需申请  WRITE_EXTERNAL_STORAGE  权限
 
权限说明
 
权限名称 用途 适配说明 
 android.permission.INTERNET  扫描网络打印机 必须授权，无系统版本限制 
 android.permission.ACCESS_WIFI_STATE  获取局域网状态 必须授权，用于网络打印机扫描 
 android.permission.READ_MEDIA_IMAGES  读取图片文件 Android 13+ 替代  READ_EXTERNAL_STORAGE  
 android.permission.READ_MEDIA_DOCUMENTS  读取文档文件 Android 13+ 适配，无需额外存储权限 
 
核心技术说明
 
1. 系统打印接口封装
- 自定义  PrintManagerWrapper  类，统一管理系统打印服务的获取、任务创建与状态监听
- 通过  PrintDocumentAdapter  实现打印文档的加载与渲染，支持多格式文件适配
2. Context 使用规范
- 全局工具类、Repository、 PrintManagerWrapper  必须使用 Application Context，禁止持有 Activity/Fragment Context
- ViewModel 需继承  AndroidViewModel  获取 Application Context，避免页面销毁导致的内存泄漏
3. Android 11 分区存储适配
- 不申请  WRITE_EXTERNAL_STORAGE  权限，打印文件通过系统文件选择器选取
- 本地任务数据存储于应用私有目录，保障数据安全性与系统兼容性
 
贡献指南
 
1. Fork 本仓库至个人 GitHub 账号（https://github.com/pacific728/Flora.git）
2. 创建功能分支（ git checkout -b feature/xxx ）
3. 提交代码（ git commit -m 'feat: add xxx function' ）
4. 推送分支（ git push origin feature/xxx ）
5. 提交 Pull Request 至主仓库，等待审核合并
 
许可证
 
本项目采用 Apache License 2.0 开源许可证，详情请参见项目根目录下的 LICENSE 文件。
 
 
 
欢迎提交 Issue 反馈 Bug 或提出功能优化建议！
