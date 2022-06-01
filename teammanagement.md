# 技术团队管理规范



### 一. 项目技术选型

#### 1.后端技术栈

​	根据项目的预计受众规模估算并发量，以及项目的开发周期，开发人员数量和实际的招聘情况来决定使用的语言和架构，不同的语言由其优缺点和特性：

​	a) Java：语言成熟，微服务架构完善，配套组件齐全，通过虚拟机模式可以实现跨平台运行，也是由于其虚拟机模式，相对下面两种语言，Java架构的程序比较占内存；

​	b) Go：新兴语言，在海量并发(超百万的QPS)上面性能优于Java语言，运行内存小于Java，开发效率优于Java，但是以2022年来讲，go开发工程师招聘难度大于Java、PHP等；

​	c) PHP: PHP在开发效率上面优于上面二者，特别是在前后端一体的项目上，但是PHP的并发性弱于其他语言，通常需要配合Swolle提高其并发性能，同时PHP语言在安全性较差；



#### 2.前端技术栈

​	前端Js框架一般采用React、Vue和Angular，具体选用哪个需要根据项目的规模，以及开发人员对于三种框架的熟悉度，以及人员的招聘难度：

​	a) React由Facebook构建，用户量比较大，并且有丰富的UI组件；

​	b) Vue由Evan You主导的社区来驱动维护，三者中比较新的框架，体积小巧，易于使用，学习成本较低；

​	c) Angular由Google构建，基于MERN架构，最适合大型的项目，性能表现较好，学习成本较高；



#### 3.APP技术栈

​	APP开发主要分为两大类，原生开发和跨平台开发，其中原生开发是最为主流的开发模式，因为其兼容性和组件的丰富性是最高的，但是其开发成本较高，需要有iOS和Android的原生语言工程师来开发和维护，而跨平台开发，市面上流行的Flutter和React则可以用一套代码打包iOS和Android的安装包，并且可以热更新，其开发效率上面优于原生开发，但是其兼容性和性能表现上面比较差，具体采用哪种开发模式，则需要根据项目规模，项目是倾向于成熟稳定还是倾向于热更新和开发效率，还有开发人员的语言熟悉度具体来决定。



#### 3.运维技术栈

​	1.1 服务器：服务器通常采用Linux服务器，除了一些特殊需求而使用Windows和Mac服务器；

​	1.2 数据库：中小型项目数据库一般采用关系型数据库MySql，大型项目使用Oracle，非关系型数据库常用的有Redis，Mongodb，Elastic Search，通常不同的非关系型数据库在使用上有不同侧重点，可多个结合一起使用，Redis主要用来做数据缓存和并发限制，Mongodb一般用来存储文档数据，Elastic Search一般用来存储日志，和需要用于搜索的数据；

​	1.3 环境部署：主要使用容器化部署或直接服务器部署，容器化部署通常使用Kubernetes+Docker，其有点是维护和扩展比较简单，直接服务器部署则在单机有多个应用程序的情况下，不同程序之间会影响稳定性，且维护麻烦；



### 二. 团队人员架构

​	技术团队人员的数量由项目数量，项目规模和需求数量决定，通常会根据职能不同区分不同部门，根据部门人数设立部门负责人，一般团队架构如下：

​	a) **技术负责人CTO**：负责统筹团队工作安排，工作质量把控，技术钻研和技术培训等；

​	b) **后端研发部门/小组**：根据需要设立部门组长，主管团队的后端研发和维护工作，一般数量是前端部门人员的两倍；

​	c) **前端研发部门/小组**：根据需要设立部门组长，主管团队的前端研发和维护工作，前端主要包括网站的PC和H5端；

​	e) **移动端研发部门/小组**：根据需要设立部门组长，主管团队的APP端研发和维护工作，移动端主要包括iOS，Android;

​	f) **客户端研发部门/小组**：根据需要设立部门组长，主管团队的桌面客户端研发和维护工作，客户端包括Windows，Mac，Linux;

​	g) **产品部门/小组**：根据需要设立部门组长，主管团队的产品策划，需求收集，产品质量把控等工作；

​	h) **美术设计部门/小组**：根据需要设立部门组长，主管团队的UI及其他美术资源的制作和维护；

​	i) **运维部门/小组**：根据需要设立部门组长，主管团队的服务器维护，办公设备管理，网络管理，代码管理，数据库管理；

​	j) **测试部门/小组**：根据需要设立部门组长，主管团队的测试工作，主要有黑白盒测试；



### 三. 工作流程规范

#### 1. 团队协作

1.1 **项目立项**：项目经理召开立项会议，与产品经理和技术经理一起沟通项目的意图与受众群体的规模，以及项目的期望上线时间，沟通完成则正式立项；

1.2 **需求整理**：立项完成，产品经理整理产品需求，与需求方进行沟通敲定需求细则，确定每一个需求的优先级，优先级分为 ”紧急“，”优先“，”正常“，紧急类需求需要优先开发上线，优先类需求作为优先考虑的需求整理在下一期的迭代版本里，正常类需求将在开发有空档的时间内迭代开发；

1.3 **需求研讨**：需求整理完成，产品根据整理的下一期的版本需求制作需求文档，以及产品原型图，若在业务流程比较复杂的需求则需要附带业务流程图，脑图等相关辅助图表，制作完成之后先与项目经理和产品部门负责人，技术经理进行需求研讨会，会议上各方根据自己的专业角度提出意见，产品经理根据意见修改，直至达成统一，技术经理在需求研讨完成之后，安排开发人员参与项目开发；

1.4 **需求评审**：产品经理发起会议邀请，参与人员为该版本需求的开发人员和测试人员，人员为技术经理指定，在需求评审会议上，产品经理需要详细的对需求进行讲解和答疑，产品经理要根据需求的期望上线时间，跟参与需求开发的人员沟通确定好需求从”开发"到"测试" 到上线的开发周期，以及规划开发测试验收的时间线，后面的开发流程需要严格按照时间线进行，开发完成由产品经理做最后验收，验收完成进入发布安排阶段；

1.5 **发布安排**：由技术经理安排发布时间和发布人员，如果是非上班时间则需要安排开发人员和产品人员在发布时间值守，发布人员一般为运维，运维需提前收集该期版本发布所需要的代码分支或Tag，发布流程，数据库文件，图片等文件，如果是需要停服更新，需要提前获得项目运营方同意才能进行，发布完成由产品做线上服务版本验收，验收完毕通知所有人项目上线完成，项目经理则需要通知相关运营方；

1.6 **BUG处理**：任何人在测试产品发现BUG或任何不合理的地方都可以跟产品部门提出意见，由产品经理收集并进行优先级判定，如果是非紧急bug则作为优化需求排入迭代需求，如果是紧急bug则需要告知技术经理，由技术经理安排人员优先处理并及时发布，紧急BUG处理优先于所有任务；

1.7 **沟通会议**：需求开发期间，项目小组每天早晨10-15分钟项目早会，汇报各自的工作进度以及遇到的问题，每周五的下午召开团队周会，总结一周的工作以及交流分享；



#### 2.团队规范

1.1 **使用软件**：

​	a) **项目管理**：本地服务器部署“禅道(Zentao)”开源版作为项目管理软件，项目经理立项，产品经理整理需求，测试提bug都统一使用禅道，由运维负责维护；

​	b) **文件管理**：本地服务器部署FTP作为项目文档存储，做好每个员工的权限分配，由运维负责维护；

​	c) **代码管理**：本地服务器部署Gitlab作为代码版本控制系统，由运维负责维护；

​	d) **API协作**：使用Apifox作为API协作和管理平台，每次功能上线后将API文档导出保存到FTP；



1.2 **文档规范**：

​	项目的所有文档包括但不限于以下类型，均不得在未经允许的情况下对外传播，否则将被追究法律责任。

​	a) **产品需求文档**：文档标题注明产品名称，版本号，内容需要包括功能描述，示意图，业务逻辑说明，文档存放在FTP时需要存放在指定产品指定日期的目录内；

​	b) **产品原型文稿**：文稿标题注明产品名称，版本号，内容需要包括版本说明，原型图，必要的文字说明，必要的动画，文稿存放在FTP时需要存放在指定产品指定日期的目录内；

​	c) **接口文档**：接口文档标题注明产品名称和日期，内容需要包括接口路径，参数说明，返回内容示例等，文档存放在开发专用FTP目录下的指定产品目录；

​	d) **UI文件**：UI文件包括图片和PS文稿，图片需要压缩后才给到开发，PS文稿需要注明功能，存放到FTP指定的UI目录下；



1.3 **开发规范**：

​	a) **注释**：代码需要有详细的注释，每个方法的顶部注释好方法的功能以及参数的说明，方法内的变量和每一处关键代码需要注释好步骤的说明，尽量让代码更易通过注释读懂逻辑；

​	b) **命名**：变量和类文件命名采用英文命名，不能用拼音；

​	c) **安全**：注意代码和信息的安全，接口不对外暴露过多与业务无关信息，个人操作权限不能过大，每个人的开发账号权限都要区分清楚；

​	d) **质量**：写完代码做1-3遍自检自测，确保没有问题才提交到测试部门；

​	e) **流程**：严格遵守开发流程，不在未经允许的情况下操作线上数据库，线上服务器，和线上代码；

​	f) **保密**：代码不得对外分享，也不得分享给公司内无权限查看的人员；



1.4 **网络安全规范**：

​	a) **禁止安装无关软件**：团队人员不得使用办公电脑随意下载与工作无关的软件，防止被恶意软件安装木马，给公司内网造成安全威胁；

​	b) **谨慎接收图片文档**：团队人员在接收邮件，社交媒体的图片和文件，需要跟对方做好身份核实，谨慎打开，避免接收到恶意文件；

​	c) **注意个人电脑安全**：自己的工作电脑需要设置密码，下班时如果电脑不需要工作则关闭电脑，禁止未经允许远程公司电脑；

​	d) **公司文件资料安全**：所有跟公司机密文件和账号信息相关的索取都要通过邮件申请，由技术经理审批，如果有公司人员直接通过聊天软件索要机密文件，必须电话核实身份信息才能给予；



#### **3.项目流程**

1.1 **Git流程**：

​	a) 每一项目的git分支分为主分支main，线上分支prod，测试分支test，本地分支local；

​	b) 开发先在local分支新建自己的分支进行开发，自测完毕合并到local分支发布到本地环境进行测试，本地环境自测完成将代码合并到test分支发布到测试环境；

​	c) prod分支为上线分布时的准备分支，测试和产品在测试环境测试验收完成，进入准备发布阶段，由运维将test分支代码合并到prod分支，进行手动发布；

​	d) 当发布完毕线上功能测试正常，再由运维将prod分支合并到main分支；



1.2 **开发流程**：

​	a) 项目经理立项，在禅道新建项目或在已有项目，添加需求开发任务，指派给负责的产品；

​	b) 产品经理接到任务后，在禅道创建计划，如“v1.0.0开发”，然后在计划内添加所有需求，在完成了需求评审后更新需求的工时并将需求指派给技术经理；

​	c) 技术经理再将对应的需求指派给对应的开发人员，开发人员开发完成则将需求指派给测试；

​	d) 测试和产品在测试过程中发现bug，在禅道的测试栏目提bug，将bug提交给对应的开发人员，开发人员处理完再将bug单指派回测试，测试人员复测没问题则关闭bug单；

​	e) 测试人员测试完毕由产品进行验收，验收完毕则进入待发布流程；



1.3 **发布流程**：

​	a) 开发环境部署自动发布工具，开发自行合并代码到local分支进行发布；

​	b) 测试环境由开发在群里通知运维进行合并发布，通知内容格式按照申请发布内容格式；

​	c) 正式环境的发布，需要由项目经理和技术经理协调安排发布时间和人员，由运维统一收集版本发布的所有信息，发邮件通知全体技术人员，发布完成由产品做验收，验收完毕在沟通群通知上线完成；

​	d) 发布前需要收集的内容包括，发布产品名称，环境，版本号，发布时间，代码git分支/tag，上线功能说明，数据库文件，图片资源文件等，根据具体发布情况可以减少部分内容；

​	e) **申请发布内容格式**：

​	发布产品：XXX产品

​	发布环境：测试服/正式服

​	发布需求版本：v1.0.0

​	发布时间：2022.01.01 下午3：00

​	预计耗时：1小时

​	后端代码分支：prod tag:v1.0.0

​	前端代码分支：prod tag:v1.0.0	

​	数据库文件：附件

​	图片资源：；路径：xxx/xxxx，资源见附件

​	功能说明：增加xxx功能，优化xxxx;

​	

### 四.团队文化

​	团队文化能够提高团队凝聚力和合作的默契度，让团队更有向心力，从而更好的提高团队的工作效率，推动团队的技术积累，具体可以如设立每周的技术分享会，公司的知识库，学习基金，团建活动等来打造团队文化，我觉得团队的文化重点在以下几方面：

​	a) **效率第一**：中小型团队的工作中效率第一，若有出现影响效率的流程则需要改善，切忌照搬大型企业的规章制度；

​	b) **重在沟通**：任何的工作矛盾均能在沟通中解决，沟通能够避免理解偏差导致的工作问题；

​	c) **持续学习**：每个人保持持续的学习，除了可以为团队带来新的活力和知识，也可以让自己的专业能力得到提高；

​	d) **保证质量**：保证工作时间的效率以及工作的质量，是对自己工作的负责也是对团队的负责；









# Technical Team Management Specification



### 1. Project Technology Selection

#### 1. Backend Technology Stack

We choose the development language and the project architecture base on estimated concurrency, the project's expected number of users, duration of development, the number of developers, and the actual hiring difficulty. Different languages have different advantages, disadvantages, and characteristics:

a) Java: Java is very stable, the micro-service architecture and the third-party components are complete. It can be cross-platform because of JVM, but JVM needs more memory for running the program;

b) Go: A new backend development language. Its performance is better than the Java language in massive concurrency (Over one million QPS). Its running memory is less than Java and its development efficiency is better than Java. But It will be more difficult to find go developers than Java and PHP developers;

c) PHP: PHP is better than the above two languages in development efficiency, especially in some projects that integrate front and backends, but PHP is worse than the other two languages in concurrency. So it always uses "Swolle" to improve its concurrency performance. And also PHP is not secure enough.



#### 2. Front-end Technology stack

We generally use React, Vue, and Angular these three Js Framework. Which one we choose depends on the scale of the project, the developer's familiarity with these three frameworks, and the difficulty of recruiting:

 a) React is built by Facebook, has a large number of users, and has rich UI components;

 b) Vue is built and maintained by the community led by Evan You. The newer framework among the three is small in size, easy to use, and has lower learning costs;

 c) Angular is built by Google and based on MERN architecture, it is most suitable for large-scale projects, with better performance and higher learning costs;



#### 3. APP Technology Stack

 APP development is mainly divided into two categories, native development, and cross-platform development. Native development is mainly using development mode because it has the highest compatibility and richness of components, but its development cost is high, it requires iOS Developer and android developer. Flutter and React are the popular cross-platform development frameworks. It can be packaged in iOS and Android systems with the same source code and can be updated hotly. Cross-platform is better than native development in development efficiency, but it is worse than native development in compatibility and performance. Which development mode should we use depends on the scale of the project and what we want the project tends to be, mature and stable, or hot update and development efficiency? and the language familiarity of developers. 



#### 3. OP Technology stack

 1.1 Server: we usually use Linux server and some servers use Windows and Mac servers for some special requirements;

 1.2 Database: small and medium-sized project databases generally use a relational database such as MySql.Large-scale projects use Oracle. Non-relational databases commonly include Redis, MongoDB, and Elastic Search. Usually, different non-relational databases have different focuses on the use, which can be used in combination, Redis is mainly used for data caching and concurrency restrictions, Mongodb is generally used to store document data, and Elastic Search is generally used to store logs and data that needs to be used for search;

 1.3 Environmental deployment: mainly use containerized deployment or direct server deployment. Containerized deployment usually uses Kubernetes+Docker, which is relatively simple to maintain and expand, while direct server deployment is multiple applications on a single machine. It will affect the stability and maintenance;



### 2. Team Structure

 The number of technical team members is determined by the number of projects, project scale, and the number of requests. Usually, different departments are distinguished according to different functions, and department heads are established according to the number of departments. The general team structure is as follows:

 a) **Technical Leader (CTO)**: responsible for coordinating teamwork arrangements, work quality control, technical research, technical training, etc.;

 b) **Back-end  Department**: set up a department leader if needed to supervise the back-end development and maintenance, its number is generally twice as many as the front-end department;

 c) **Front-end Department**: Set up a department leader if needed to be in charge of the front-end development and maintenance. The front-end mainly includes the PC and H5 client of the website;

 e) **Mobile Department**: Set up a department leader if needed to be in charge of the APP development and maintenance. The mobile client mainly includes iOS and Android;

 f) **Client Department**: Set up a department leader if needed to supervise the team’s desktop client development and maintenance work, clients include Windows, Mac, and Linux;

 g) **Product Department**: Set up a department leader as needed to supervise the team’s product planning, requirements collection, product quality control, etc.;

 h) **Art Design Department**: Set up a department leader if needed to be in charge of the production and maintenance of the team’s UI and other art resources;

 i) **OP Department**: set up a department leader if needed to be in charge of the team’s server maintenance, office equipment management, network management, code management, and database management;

 j) **QA Department**: Set up a department leader if needed to supervise the testing work of the team, mainly black and white box testing;



### 3. Workflow Specification

#### 1. Teamwork

1.1 **Project Approval**: The project manager will hold a project approval meeting to communicate with the product manager and technical manager the intent of the project, the number of the users, and the expected deployment time of the project. After the communication is completed, the project will be officially approved;

1.2 **Requirements Sorting**: After the project is approved, the product manager organizes the product requirements, communicates with the demander to finalize the details of the requirements, and determines the priority of each requirement. The priority is divided into "urgent", "priority", and "normal", Urgent requirements need to be developed and deployed first, priority requirements will be sorted out in the next version of the project, and normal requirements will be iteratively developed when there is a gap in development;

1.3 **Requirement Discussion**: After the requirements are sorted out, the product manager will produce the requirements document according to the sorted version requirements of the next version, as well as the product prototype diagram. If the business process is more complex, it needs to be accompanied by a business flow chart, a brain map, etc. After the production is completed, firstly have a meeting with the project manager, the product department leader, and the technical manager. At the meeting, all parties put forward opinions according to their professional perspectives, and the product manager revises according to the opinions until a consensus is reached, and the technical manager will arrange for developers to participate in project development after the meeting;

1.4 **Requirements Review**: The product manager initiates a meeting invitation, the participants are the developers and testers of the version requirements who are designated by the technical manager. At the requirements review meeting, the product manager needs to explain and answer questions in detail about the requirements, the product manager should communicate with the developer to make sure the development duration from "development" to "test" to "deploy" of the requirements according to the expected deploy time, and plan the timeline for development, testing, and acceptance. The subsequent development process needs to strictly follow the timeline. The product manager will make the final acceptance after the development is completed and the requirements will enter the release arrangement stage;

1.5 **Deployment Arrangement**: The Technical manager will arrange the release time and the person to handle the deployment. If it is not working hours, developers and PM should be arranged to be on duty during the deployment time. The code branch or Tag, release process, database files, pictures, and other files required for the release if it is necessary to stop the service need to obtain the approval of the project operator in advance. The project manager needs to notify the relevant operators after deployment is completed；

1.6 **Bug Handling**: Anyone who finds a bug or any unreasonable issue in the test should report it to the product department, and the product manager will collect and determine the priority. If it is a non-urgent bug, it will be put into the iteration as an optimization requirement. If it is an emergency bug need to inform the technical manager, and the technical manager will arrange a person to fix it and deploy it first. Emergency bug processing takes priority over all tasks;

1.7 **Communication Meeting**: During the required development time, the project team will have a 10-15 minute morning meeting every morning to report their work progress and problems, and hold a weekly team meeting every Friday afternoon to summarize the work of the week and share the information;



#### 2. Team Specifications

1.1 **Using Software**:

 a) **Project Management**: The open-source version of "Zentao" is deployed on the local server as project management software. "Zentao" is used for establishing the project by the project manager, organizing the requirements by the product manager, and managing bugs by QA. It is maintained by the OP department ;

 b) **File Management**: FTP is deployed on the local server as the project document storage, and the authority assignment of each employee is done well, and the OP department is responsible for the maintenance;

 c) **Code Management**: The local server deploys Gitlab as the code version control system, which is maintained by the OP department;

 d) **API Collaboration**: Use Apifox as the API collaboration and management platform, export and save API documents to FTP after each function goes online;



1.2 **Document Specifications**:

 All documents of the project, including but not limited to the following types, must not be disseminated without permission, otherwise, legal responsibility will be pursued.

 a) **Product Requirements Document**: The title of the document indicates the product name, and version number, and the content needs to include a functional description, schematic diagram, and business logic description. When the document is stored in FTP, it needs to be stored in the directory on the specified date of the specified product;

 b) **Product Prototype Manuscript**: The title of the manuscript should indicate the product name, version number, and the content should include a version description, prototype diagram, necessary text description, necessary animation, and when the manuscript is stored in FTP, it should be stored in the designated product designated within the directory of the date;

 c) **API Document**: The title of the API document indicates the product name and date, and the content needs to include the API path, parameter description, return content example, etc. The document is stored in the designated product directory under the development-specific FTP directory;

 d) **UI file**: UI files include pictures and PS files. The pictures need to be compressed before they can be developed. The PS files need to indicate functions and store them in the UI directory specified by FTP;



1.3 **Development Specifications**:

 a) **Comment**: The code needs to have detailed comments. The top of each method is annotated with the function of the method and the description of the parameters. The variables in the method and each keycode need to be annotated with the description of the steps. The code is easier to understand the logic through comments;

 b) **Naming**: variables and class files are named in English, not Pinyin;

 c) **Security**: Pay attention to the security of code and information, the interface should not expose too much information irrelevant to the business, the personal operation authority should not be too large, and the development account authority of each person should be distinguished;

 d) **Quality**: After writing the code, do 1-3 times of self-testing and self-testing to ensure that there are no problems before submitting it to the testing department;

 e) **Process**: Strictly abide by the development process, do not operate online databases, online servers, and online codes without permission;

 f) **Confidentiality**: The code shall not be shared externally, nor shall it be shared with persons in the company who do not have permission to view it;



1.4 **Network Security Specifications**:

 a) **Installation of Irrelevant Software is Prohibited**: Team members are not allowed to use office computers to download software unrelated to work at will, to prevent Trojan horses from being installed by malicious software and causing security threats to the company’s intranet;

 b) **Receive Pictures and Documents with Caution**: When team members receive emails, pictures, and documents from social media, they need to verify their identity with the other party, open them carefully, and avoid receiving malicious documents;

 c) **Pay Attention to Personal Computer Security**: You need to set a password for your work computer. If the computer does not need to get off work when you get off work, turn off the computer, and it is forbidden to remote company computers without permission;

 d) **Company Document Data Security**: All requests related to the company’s confidential documents and account information must be applied by email and approved by the technical manager. If any company personnel directly ask for confidential documents through chat software, they must call to verify their identity information can be given;



#### **3. Project Process**

1.1 **Git Process**:

 a) The git branch of each project is divided into the main branch, the prod branch, the test branch, and the local branch;

 b) For development, first create your branch in the local branch. After the self-test is completed, merge it into the local branch and publish it to the local environment for testing. After the local environment self-test is completed, merge the code into the test branch and publish it to the test environment;

 c) The prod branch is the preparation branch for online distribution. The tests and products are tested and accepted in the test environment and enter the preparation release stage. The OP department will merge the test branch code into the prod branch for manual release;

 d) When the online functional test is normal after the release, the OP department will merge the prod branch into the main branch;



1.2 **Development Process**:

 a) The project manager establishes a project, creates a new project in Zendao or adds a requirement development task to an existing project, and assigns it to the responsible PM;

 b) After the pm receives the task, create a plan in ZenTao, such as "v1.0.0 development", then add all the requirements in the plan, update the working hours of the requirements after completing the requirements review and assign the requirements to the technical manager;

 c) The technical manager will then assign the corresponding requirements to the corresponding developers, and the developers will assign the requirements to the test after the development is completed;

 d) If bugs are found during testing and product testing, report bugs in ZenTao’s testing section and submit the bugs to the corresponding developers. After the developers have dealt with them, they will assign the bugs back to the test. If there is no problem with the testers’ retesting then close the bug ticket;

 e) After the testers have completed the test, the PM will be accepted for acceptance, and after the acceptance is completed, it will enter the process to be released;



1.3 **Publishing Process**:

 a) The development environment has the automatic release tool so the developers can merge the code to the local branch for release;

 b) The test environment is merged and released by the OP after receiving the requirement from the developer. The format of the requirement is following the format of the publishing content;

c) For the release of the official environment, the project manager and the technical manager need to coordinate and arrange the release time and personnel. The OP will collect all the information about the version release, and send an email to notify all the technical personnel. After the release is completed, the product will be checked and accepted by PM and send a confirmation message to the communication group when it is completed;

 d) The content that needs to be collected before release includes the release product name, environment, version number, release time, code git branch/tag, online function description, database file, image resource file, etc. Some content can be reduced according to the specific release situation;

 e) **Format of Publishing Content**:

 Products: XXX products

 Environment: test server/official server

 Requirement version: v1.0.0

 Publish Time: 2022.01.01 3:00 pm

 Estimated Duration: 1 hour

 Backend Code Branch: prod tag:v1.0.0

 Front-end Code Branch: prod tag:v1.0.0

 Database File: see the attachment

 Image Resource: path: xxx/xxxx.png, see the attachment for the resource

 Description: add xxx function, optimize xxxx;



### 4. Team Culture

 Team culture can improve team cohesion and tacit understanding of cooperation, and make the team more cohesive, thereby better improving the team’s work efficiency and promoting the team’s technology accumulation. Specifically, such as setting up weekly technology sharing meetings, the company’s knowledge base, learning funds, team building activities, etc. to build team culture, I think the focus of team culture is in the following aspects:

 a) **Efficiency First**: Efficiency comes first in the work of small and medium-sized teams. If there is a process that affects efficiency, it needs to be improved. Do not copy the rules and regulations of large enterprises;

 b) **Focus on Communication**: any work conflict can be resolved in communication, and communication can avoid work problems caused by misunderstanding;

 c) **Continuous Learning**: Everyone maintains continuous learning, which can not only bring new vitality and knowledge to the team but also improve their professional ability;

 d) **Maintain quality**: ensure the efficiency of working hours and the quality of work, which is responsible for your work and the team;
