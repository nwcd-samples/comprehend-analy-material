# 基于Comprehend的玩家评论分析解决方案

如今，在一个互联网高度发达的社会中，人们的娱乐方式更多的由线下转为线上，而更好的游戏体验无疑是吸引更多的游戏玩家首要因素，而一个游戏的成功与否不仅仅是在于游戏产品设计师和游戏开发者的设计，更多的是在后续的游戏版本更迭中，更多的保留吸引用户的元素和用户喜爱的环节，去除用户不喜欢的元素，改掉用户提出的缺点。而如今游戏民意的收集却是广大游戏开发者和设计者的难题，原因一是在于游戏发布平台的非常广，且需要分别根据游戏名称，国家和版本进行分别归类，二是在于对于评论文字的分析并从中提取出用户的情绪和关键字，从而得知游戏的优缺点，这其实是一项基于机器学习自然语言处理的任务，需要专业的自然语言处理相关的算法工程师进行解决，由此投入不菲的人力物力。基于Comprehend 的玩家评论分析解决方案分别抓取Apple App Store 和Google Play这两大主流游戏发行平台的评论数据，并利用Comprehend—AWS托管的自然语言处理服务，进行情绪分析和关键词检测，定期抓取新增评论并进行分析，最终实现在QuickSight的可视化面板中展示分析结果。该解决方案可使用Cloudformation 快速部署，帮助用户快速实现对游戏评论分析的需求。

##解决方案概述

此解决方案使用户可以快速在AWS 云上构建高可用和无服务器的玩家评论分析系统，用以实现对不同版本，不同国家游戏玩家体验的收集和分析，用于阶段性总结游戏的优势与缺点，为游戏的更迭和更好的吸引客户打下基础。该解决方案使用Fargate作为无服务器容器计算服务运行抓取代码，借助AWS Fargate，您无需预置和管理容器实例，相关代码逻辑会在初始化过程中和之后每天一次的频率由Cloudwatch自动触发运行，运行过程中会读取存储在S3中的相关游戏信息文件。CloudWatch是AWS的管理监控服务，本解决方案中，由CloudWatch配置定时任务规则，以便每天更新新的评论数据分析。另外，本解决方案使用Aurora Serverless版本作为系统数据库，用于存储抓取的评论数据和相关信息。Aurora Serverless 数据库集群会根据您应用程序的需求自动启动、关闭以及扩展或缩减容量，非常适合这种不频发的工作负载，同时大幅节省了成本。数据库表结构的初始化工作由Lambda完成。Lambda是AWS的无服务计算服务，无需预置或管理服务器即可运行代码。可以设置为自动从其他 AWS 产品触发，只需按使用的计算时间付费， Lambda 在本解决方案中由Cloudformation自动部署脚本触发执行数据库初始化的工作。对于本解决方案的核心，文本分析功能，我们使用Amazon Comprehend作为提取文本的分析工具，用于提取语句的关键词和情感倾向。Amazon Comprehend 是一项自然语言处理 (NLP) 服务，可通过机器学习发现文本中的见解和关系。不需要有机器学习经验。Comprehend拥有关键词提取，情绪分析，实体识别等诸多功能，可以分析一系列文本文件，并自动按相关术语或主题对它们进行整理，还可以基于自己的业务逻辑设置自定义标签，并基于此进行自定义文本分类，从而为客户提供个性化内容。可以用于客户意见分析，知识管理等多种场景。本解决方案中，Comprehend用于分析出文本中的实体，关键字和情感，便于统计和分析游戏的玩家反馈。更多关于Comprehend的功能请参考：https://docs.aws.amazon.com/zh_cn/comprehend/latest/dg/comprehend-general.html



##免责声明

建议测试过程中使用此方案，生产环境使用请自行考虑评估。
当您对方案需要进一步的沟通和反馈后，可以联系 nwcd_labs@nwcdcloud.cn 获得更进一步的支持。
欢迎联系参与方案共建和提交方案需求, 也欢迎在 github 项目 issue 中留言反馈 bugs。

