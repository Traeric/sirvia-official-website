<template>
    <div>
        <div id="top">
            <div class="left">
                <div class="logo">
                    <img src="../assets/images/logo-content.png" alt="NO IMG">
                </div>
            </div>
            <div class="right">

            </div>
        </div>
        <div id="bottom">
            <div class="left">
                <div class="select-version">
                    <h2>版本</h2>
                    <el-select v-model="selectVersion" placeholder="活动区域">
                        <el-option label="区域一" value="0"></el-option>
                        <el-option label="区域二" value="1"></el-option>
                    </el-select>
                </div>
                <div class="title"><h2>目录</h2></div>
                <div class="menu">
                    <el-menu
                            default-active="2"
                            class="el-menu-vertical-demo"
                            @open="handleOpen"
                            @close="handleClose">
                        <el-submenu index="1">
                            <template slot="title">
                                <i class="el-icon-location"></i>
                                <span>导航一</span>
                            </template>
                            <el-menu-item-group>
                                <template slot="title">分组一</template>
                                <el-menu-item index="1-1">选项1</el-menu-item>
                                <el-menu-item index="1-2">选项2</el-menu-item>
                            </el-menu-item-group>
                            <el-menu-item-group title="分组2">
                                <el-menu-item index="1-3">选项3</el-menu-item>
                            </el-menu-item-group>
                            <el-submenu index="1-4">
                                <template slot="title">选项4</template>
                                <el-menu-item index="1-4-1">选项1</el-menu-item>
                            </el-submenu>
                        </el-submenu>
                        <el-menu-item index="2">
                            <i class="el-icon-menu"></i>
                            <span slot="title">导航二</span>
                        </el-menu-item>
                        <el-menu-item index="3" disabled>
                            <i class="el-icon-document"></i>
                            <span slot="title">导航三</span>
                        </el-menu-item>
                        <el-menu-item index="4">
                            <i class="el-icon-setting"></i>
                            <span slot="title">导航四</span>
                        </el-menu-item>
                    </el-menu>
                </div>
            </div>
            <div class="right">
                <div class="content" ref="content">
                    <h2 id="起步">起步</h2>
                    <h3 id="1-导入依赖">1. 导入依赖</h3>
                    <pre><code class="language-xml">&lt;dependency&gt;
    &lt;groupId&gt;io.github.traeric.sirvia&lt;/groupId&gt;
    &lt;artifactId&gt;lsirvia&lt;/artifactId&gt;
    &lt;version&gt;0.1.2-RELEASE&lt;/version&gt;
&lt;/dependency&gt;</code></pre>
                    <p>使用Sirvia第一步需要导入对应的maven依赖</p>
                    <h3 id="2配置webxml">2.配置web.xml</h3>
                    <p>
                        由于Sirvia使用了shiro做认证，所以需要在web.xml中配置shiroFilter，当然由于Sirvia也使用了Spring跟SpringMVC，所以需要配置DispatcherServlet跟spring配置文件</p>
                    <pre><code class="language-xml">&lt;filter&gt;
    &lt;filter-name&gt;shiroFilter&lt;/filter-name&gt;
    &lt;filter-class&gt;org.springframework.web.filter.DelegatingFilterProxy&lt;/filter-class&gt;
    &lt;init-param&gt;
        &lt;param-name&gt;targetFilterLifecycle&lt;/param-name&gt;
        &lt;param-value&gt;true&lt;/param-value&gt;
    &lt;/init-param&gt;
&lt;/filter&gt;
&lt;filter-mapping&gt;
    &lt;filter-name&gt;shiroFilter&lt;/filter-name&gt;
    &lt;url-pattern&gt;/*&lt;/url-pattern&gt;
&lt;/filter-mapping&gt;</code></pre>
                    <h3 id="3导入sirvia的spring以及springmvc配置文件">3.导入Sirvia的spring以及springMVC配置文件</h3>
                    <p>
                        分别找到当前项目的spring以及SpringMVC配置文件，并在其中导入Sirvia的相关配置文件，当然，如果你的项目只有一个spring的配置文件，也可以将两项配置全部导入到这一个spring配置文件中</p>
                    <p><code>在当前项目的spring配置文件中导入Sirvia的spring配置文件（applicationContext.xml）</code></p>
                    <pre><code
                            class="language-xml">&lt;import resource="classpath*:adminApplicationContext.xml" /&gt;</code></pre>
                    <p><code>在当前项目的springMVC配置文件中导入Sirvia的springMVC配置文件（dispatcher-servlet.xml）</code></p>
                    <pre><code
                            class="language-xml">&lt;import resource="classpath*:springMVC-servlet.xml"/&gt;</code></pre>
                    <h3 id="4配置数据库">4.配置数据库</h3>
                    <p>由于Sirvia是用于操作数据库的工具，所以需要连接你的数据库，因此需要在你项目的spring配置文件中配置数据库的相关信息。</p>
                    <p>
                        在配置之前需要提一个东西，就是<code>CommonsSetting</code>类，这个类是用于你的项目与Sirvia进行通信的，所以数据库信息需要设置在这个类中，你可以自己新建一个类继承<code>CommonsSetting</code>类，也可以直接在Spring配置文件中配置这个类
                    </p>
                    <pre><code class="language-xml">&lt;bean name="commonsSetting" class="com.ericjin.javadmin.CommonsSetting"&gt;
    &lt;property name="dataBase"&gt;
        &lt;map&gt;
            &lt;entry key="url" value="jdbc:mysql://127.0.0.1:3306/java_admin?serverTimezone=UTC"/&gt;
            &lt;entry key="password" value="root"/&gt;
            &lt;entry key="user" value="root"/&gt;
            &lt;entry key="driver" value="com.mysql.jdbc.Driver"/&gt;
        &lt;/map&gt;
    &lt;/property&gt;
&lt;/bean&gt;</code></pre>
                    <p>注意bean的名称不要改变</p>
                    <p>此时，启动项目如果成功，就表示已经引入Sirvia成功了</p>
                    <p>访问：<code>/admin/login</code>就可以来到登陆页面，如下</p>
                    <p><img src="../assets/images/login.png" alt="NO IMG"></p>
                    <h2 id="功能介绍">功能介绍</h2>
                    <p>想要使用Sirvia，还需要有一个账户</p>
                    <h3 id="1-生成user表以及账户">1. 生成user表以及账户</h3>
                    <p>想要进入Sirvia页面管理数据表需要登陆，那么首先需要创建账户，账户存储在数据库中，因此需要先创建用户表，具体的创建是在<code>Generate</code>类中完成的</p>
                    <p>在当前的项目中准备一个类，在类的<code>main</code>方法中执行<code>Generate</code>的<code>generateUserTable()</code>方法来创建用户表，方法需要传入数据库信息，按需传入即可。
                    </p>
                    <pre><code class="language-java">public class Test {
    public static void main(String[] args) {
        new Generate().generateUserTable("com.mysql.jdbc.Driver",
                "jdbc:mysql://127.0.0.1:3306/java_admin?serverTimezone=UTC",
                "root", "root");
    }
}</code></pre>
                    <p>创建用户表后就需要创建账户了，还是在该类的<code>main</code>方法中执行<code>Generate</code>的<code>createUser()</code>方法，按照要求填写即可创建账户。
                    </p>
                    <pre><code class="language-java">public class Test {
    public static void main(String[] args) {
        new Generate().createUser("com.mysql.jdbc.Driver",
                "jdbc:mysql://127.0.0.1:3306/java_admin?serverTimezone=UTC",
                "root", "root");
}</code></pre>
                    <p><img src="../assets/images/create_user.png" alt="NO IMG"></p>
                    <h3 id="2-登陆java-admin">2. 登陆Java admin</h3>
                    <p>启动项目后，通过地址<code>http://127.0.0.1:8080/admin/login</code>可以进入Sirvia的登陆页面，如下：</p>
                    <p><img src="../assets/images/login.png" alt="NO IMG"></p>
                    <h3 id="3-操作数据表">3. 操作数据表</h3>
                    <p>登陆后会进入首页，首页展示如下：</p>
                    <p><img src="../assets/images/index.png" alt="NO IMG"></p>
                    <p>可以看到，首页有一个Panel，Panel的头部写着系统表，这是Sirvia系统自带的表，可以看到有一张用户表，这张表就是刚刚第二步通过<code>Generate</code>类创建的表，里面存储有用户信息，一般不是太会用到。那么如果想要操作自己的表应该怎么做呢？
                    </p>
                    <p>在你的项目中能够被spring扫描的包内创建一个类，这里命名为<code>MyRegister</code>，它需要继承<code>Register</code>类，如果需要将自己的表交给Sirvia管理，需要重写<code>userTableList()</code>方法，在方法中接收父类方法的列表，将需要自己表对应的实体类的Class对象添加到这个列表中，然后将这个列表返回出去
                    </p>
                    <pre><code class="language-java">public class MyRegister extends Register {
    @Override
    public List&lt;Class&gt; userTableList() {
        List&lt;Class&gt; list = super.userTableList();
        list.add(Article.class);
        list.add(Tags.class);
        list.add(Test.class);
        return list;
    }
}</code></pre>
                    <p>然后将该列表放到spring容器中，即在applicationContext.xml文件中加入如下代码</p>
                    <pre><code class="language-xml">&lt;!-- 这里的MyRegister就是刚刚创建的，包路径填写自己的 --&gt;
&lt;bean name="my_register" class="com.jinxin.MyRegister"/&gt;
&lt;!-- 这里注意名字不能改变，必须是userTableList --&gt;
&lt;bean name="userTableList" factory-bean="my_register" factory-method="userTableList"/&gt;</code></pre>
                    <p>在上面的代码中添加了三个实体类，注意添加的实体类一定要在数据库中有对应的表。</p>
                    <p>重启项目，然后来到首页：</p>
                    <p><img src="../assets/images/index-user.png" alt="NO IMG"></p>
                    <p>可以看到，刚刚添加的三个表已经在首页展示了</p>
                    <h4 id="查询数据">查询数据</h4>
                    <p>可以看到在系统表下面有了一个用户表，里面有三条信息，正是刚刚添加的三个实体类，可以点进去进行查看，例如现在点进<code>Article</code>中：</p>
                    <p><img src="../assets/images/list.png" alt="NO IMG"></p>
                    <h4 id="添加数据">添加数据</h4>
                    <p>点进去后就是关于Article的所有数据了，在这里面可以针对每一条数据进行修改，也可以添加Article，只需要点击绿色的按钮即可，点击后会出现下面的页面：</p>
                    <p><img src="../assets/images/add.png" alt="NO IMG"></p>
                    <p>​ Sirvia会根据<code>Article</code>实体类中的所有私有属性进行表单渲染，表单类型会根据属性的类型来选择渲染，或input框，或select框，或radio框，或穿梭框等等。
                    </p>
                    <p>​ 如果在该实体类中有外键关联了其他的实体类，Sirvia会找到所关联的表的所有字段渲染成一个select框供选择，显示外键的属性上面需要标注<code>@ForeignKey</code>注解，在注解里面可以配置要显示的字段名以及要保存的外键value。如果是多对多，则会渲染成穿梭框，需要在属性上标注<code>@ManyToManyField</code>注解，注解里面的内容后面会详细说明。
                    </p>
                    <p>​ 在上图中可以看到不论是外键还是多对多的旁边都有一个添加按钮，点击这个按钮就可以往对应的关联表的中添加信息，例如上图中点击按钮就可以对tag表进行添加，如下：</p>
                    <p><img src="../assets/images/add_foreign.png" alt="NO IMG"></p>
                    <p>在上图中的红框中就是添加tag的页面，填写后保存即可。</p>
                    <h4 id="修改跟删除数据">修改跟删除数据</h4>
                    <p>再回到数据展示页面，可以看到在每一条数据后面都有一个编辑按钮，点击进入：</p>
                    <p><img src="../assets/images/edit.png" alt="NO IMG"></p>
                    <p>
                        可以看到和添加表的页面基本没有差别，只是在每一个输入框中都已经填入了已经保存在数据库中的信息，还有就是在底部添加了一个删除按钮，点击删除就可以对该条数据进行删除，其他都与添加页面的功能保持一致。</p>
                    <h4 id="action">Action</h4>
                    <p>Action是一个可以对数据进行批量操作的功能，在数据展示页面，选中要批量操作的数据，然后在Action选框中选中要进行何种批量操作，最后点击执行即可。如下：</p>
                    <p><img src="../assets/images/action.png" alt="NO IMG"></p>
                    <p>Sirvia系统只提供了一个批量删除的操作，如果需要实现其他的批量操作，可以在<code>Action</code>类中自己定义，关于自定义Action的具体内容会在后面说明。</p>
                    <h2 id="sirvia注解">Sirvia注解</h2>
                    <h2 id="类注解">类注解</h2>
                    <h3 id="entitytablename">EntityTableName</h3>
                    <p>EntityTableName标注在实体类上面，它的作用是标明该实体类对应着数据库中的哪张表，如果不标注，Java
                        Admin会按照实体类名的小写的方式确定表名，例如：<code>Article</code>会转换成<code>article</code>去数据库查询</p>
                    <h3 id="showname">ShowName</h3>
                    <p>这个注解的作用是为实体类重命名，在Java Admin中会按照实体类的名称来显示，如果希望显示自定义的名称，则可以通过该注解来实现。例如，现在在Java
                        Admin中显示的名字是实体类名：</p>
                    <p><img src="../assets/images/showname_entity.png" alt="NO IMG"></p>
                    <p>现在在Article类上面标注ShowName注解</p>
                    <pre><code class="language-java">@ShowName(name = "文章表")
public class Article {}</code></pre>
                    <p>再次来到首页查看：</p>
                    <p><img src="../assets/images/showname_name.png" alt="NO IMG"></p>
                    <p>可以看到，现在显示的名称已经变成了刚刚在ShowName中注解的名称</p>
                    <h2 id="字段注解">字段注解</h2>
                    <h3 id="id">Id</h3>
                    <p>id注解起初出现的意义是为了屏蔽id字段，因为大多数情况下，id是自增的，因此并不需要自己填写，所以为了避免误填，可以在id字段上面标注<code>@Id</code>注解来屏蔽掉该字段，屏蔽后再添加或者修改数据就不会出现添加id的项了。当然这个注解并不仅仅是可以添加在id字段上，还可以添加在任何想要屏蔽的字段上。
                    </p>
                    <h3 id="password">Password</h3>
                    <p>该注解也是用于标注在字段上面的，一般标注在表示密码的字段上，表示在生成input框的时候type=password</p>
                    <h3 id="dateuse">DateUse</h3>
                    <p>该注解的作用与Password注解相似，一般标注在表示日期的字段上面，表示在生成input框的时候生成日期选择的输入框</p>
                    <h3 id="choose">Choose</h3>
                    <p>有的时候一些字段只有规定的几个值需要填，例如性别字段就只有男女两个选择，这个时候就可以使用<code>Choose</code>注解去规定生成select选择框。它有几个值需要填写：</p>
                    <ul>
                        <li>type：这个字段用于确定复选框的类型，有0跟1两个选择，默认为0，0表示生成radio框，1表示生成select框；</li>
                        <li>valueList：选择框的value值；</li>
                        <li>textList：选择框要显示的文字信息；</li>
                    </ul>
                    <p><strong>type=0</strong></p>
                    <p>下面演示type=0的效果，也就是生成radio框</p>
                    <pre><code class="language-java">@ShowName(name = "文章表")
public class Article {
    @Choose(valueList = {"0", "1"}, textList = {"男", "女"})
    public Integer gender;
}</code></pre>
                    <p>生成的input框如下：</p>
                    <p><img src="../assets/images/choose_radio.png" alt="NO IMG"></p>
                    <p><strong>type=1</strong></p>
                    <p>下面演示type=1的效果，也就是生成select框</p>
                    <pre><code class="language-java">@ShowName(name = "文章表")
public class Article {
    @Choose(type = 1, valueList = {"0", "1"}, textList = {"男", "女"})
    public Integer gender;
}</code></pre>
                    <p>生成的input框如下：</p>
                    <p><img src="../assets/images/choose_select.png" alt="NO IMG"></p>
                    <h3 id="foreignkey">ForeignKey</h3>
                    <p>这个注解标注在表示外键的字段上面，标注该字段后，在添加或者编辑信息的时候会自动加载所关联的表的信息，以供选择。它有几个值需要填写：</p>
                    <ul>
                        <li>relation_table：这个值需要填写外键关联的表名；</li>
                        <li>relation_key：外键关联的表的字段，默认是<code>id</code>，这个会作为select框的value值；</li>
                        <li>show_field：想要显示关联表的哪一列的内容，这个会作为select框中的option标签体里的内容；</li>
                        <li>relation_bean：关联的表对应的实体类；</li>
                    </ul>
                    <p><strong>示例：</strong></p>
                    <pre><code class="language-java">@ForeignKey(relation_table = "tags", relation_key = "id", show_field = "name", relation_bean = Tags.class)
private Integer tag;</code></pre>
                    <p>生成的表单如下：</p>
                    <p><img src="../assets/images/foreignkey.png" alt="NO IMG"></p>
                    <h3 id="manytomanyfield">ManyToManyField</h3>
                    <p>这个注解标注在多对多关联的字段上，会显示一个穿梭框，它会自动加载第三张表的信息以供选择。它有几个值需要填写：</p>
                    <ul>
                        <li>relation_table：关联的表的表名；</li>
                        <li>third_table：多对多会出现第三张表，这个字段填写第三张表的表名；</li>
                        <li>show_field：想要显示关联表哪一列的内容；</li>
                        <li>relation_field：关联表在第三张表中插入的内容，一般是关联表的<code>id</code></li>
                        <li>third_relation_field：关联表在第三张表中对应的字段，也就是说该字段是一个外键，关联着关联表的id(默认)</li>
                        <li>third_self_field：当前表在第三张表中对应的字段，也就是说该字段是一个外键，关联着当前表的id(默认)</li>
                        <li>insert_field：当前表在第三张表中插入的内容，一般是本表的<code>id</code></li>
                        <li>relation_bean：当前表关联的表所对应的实体类</li>
                    </ul>
                    <p><strong>示例：</strong></p>
                    <pre><code class="language-java">@ManyToManyField(relation_table = "tags", third_table = "tag_article", show_field = "name", relation_field = "id",
            third_relation_field = "tag_id", third_self_field = "article_id", relation_bean = Tags.class)
private List tags;</code></pre>
                    <p>生成的穿梭框如下：</p>
                    <p><img src="../assets/images/manytomanyfield.png" alt="NO IMG"></p>
                    <h1 id="action-1">Action</h1>
                    <p>Sirvia还有一个比较重要的功能，就是对数据进行批量处理，在上面已经提到了批量删除一些字段，那么如果想要实现一些其他的批量操作的功能应该怎么办呢？</p>
                    <p>首先需要在自己的项目中创建一个<code>MyAction</code>类，该类需要继承<code>Action</code>类，在该类中定义需要批量执行的方法</p>
                    <pre><code class="language-java">public class MyAction extends Action {
    public Boolean getNum(List&lt;Integer&gt; selectArr, String tableName, SuperMapper superMapper) {
        System.out.println("一共选中了" + selectArr.size() + "条数据");
        selectArr.forEach(System.out::println);
        return true;
    }
}</code></pre>
                    <p>然后你需要让Sirvia知道你的Action的位置，告诉Sirvia位置后，Sirvia才能帮助你执行Action里面的方法</p>
                    <p>告诉Sirvia的方法就是自定义一个类继承<code>CommonsSetting</code>类，重写<code>actionPackage()</code>方法，将自定义的Action类的路径返回出去
                    </p>
                    <pre><code class="language-java">public class MyCommonsSetting extends CommonsSetting {
    @Override
    public String actionPackage() {
        return "com.jinxin.MyAction";
    }
}</code></pre>
                    <p>将该类注册到Spring容器中，不过在开始配置数据库的时候就已经将该类注册到了容器中了，但是如果在配置数据库的时候不是使用的自定义的类而是使用Sirvia提供的<code>CommonsSetting</code>类的话就需要在这里进行替换，替换为自己的类
                    </p>
                    <pre><code class="language-xml">&lt;bean name="commonsSetting" class="com.jinxin.MyCommonsSetting"&gt;
    &lt;property name="dataBase"&gt;
        &lt;map&gt;
            &lt;entry key="url" value="jdbc:mysql://127.0.0.1:3306/java_admin?serverTimezone=UTC"/&gt;
            &lt;entry key="password" value="root"/&gt;
            &lt;entry key="user" value="root"/&gt;
            &lt;entry key="driver" value="com.mysql.jdbc.Driver"/&gt;
        &lt;/map&gt;
    &lt;/property&gt;
&lt;/bean&gt;</code></pre>
                    <p>除此之外，还需要将刚刚的批量操作展示在页面上，这需要你去<code>MyRegister</code>类中重写<code>actionMap()</code>方法，继承父类的map，然后将刚刚定义的批量删除的方法名跟要展示在页面上的操作名称放入map中，然后返回出去
                    </p>
                    <pre><code class="language-java">@Override
public Map&lt;String, String&gt; actionMap() {
    Map&lt;String, String&gt; map = super.actionMap();
    map.put("getNum", "打印所选数据的信息");
    return map;
}</code></pre>
                    <p>然后将map放到spring容器中</p>
                    <pre><code class="language-xml">&lt;bean name="my_register" class="com.jinxin.MyRegister"/&gt;
&lt;bean name="actionMap" factory-bean="my_register" factory-method="actionMap"/&gt;</code></pre>
                    <p>现在重启项目来到数据展示页：</p>
                    <p><img src="../assets/images/add_action.png" alt="NO IMG"></p>
                    <p>现在选中执行：</p>
                    <p><img src="../assets/images/do_action.png" alt="NO IMG"></p>
                    <p>成功打印所选数据的id信息</p>
                    <h1 id="执行sql">执行SQL</h1>
                    <h2 id="获取所有的表名">获取所有的表名</h2>
                    <p>在Java Admin的首页右侧还提供了两个功能，一个是获取当前连接的数据库的所有表名</p>
                    <p><img src="../assets/images/get_all_table.png" alt="NO IMG"></p>
                    <p>点击获取表即可获取数据</p>
                    <p><img src="../assets/images/get_all_tables-execute.png" alt="NO IMG"></p>
                    <h2 id="执行sql-1">执行SQL</h2>
                    <p>如果需要创建表，可以到执行sql的面板执行创建表的操作</p>
                    <p><img src="../assets/images/execute_sql.png" alt="NO IMG"></p>
                    <p>将sql数据textarea中，然后点击执行即可</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    // import {documentContent} from "../assets/js/document/0.1.2";
    // import Marked from "marked";

    export default {
        data() {
            return {
                selectVersion: "0",
            };
        },
        // mounted() {
        //     this.$refs.content.innerHTML = Marked(documentContent);
        // }
    }
</script>

<style scoped>
    #top {
        height: 60px;
        width: 100%;
        border-bottom: 1px solid #ececec;
        overflow: hidden;
        position: fixed;
        top: 0;
        background-color: #fff;
        z-index: 1000;
    }

    #top .left .logo {
        height: 50px;
        margin-top: 5px;
        margin-left: 50px;
    }

    #top .left .logo img {
        height: 100%;
    }

    #top .left {
        float: left;
    }

    #top .right {
        float: right;
    }

    #bottom {
        display: flex;
        margin-top: 60px;
    }

    #bottom .left {
        margin: 20px 10px;
        width: 275px;
        position: fixed;
        top: 60px;
        left: 0;
    }

    #bottom .left .select-version {
        display: flex;
        align-content: center;
        justify-content: center;
    }

    #bottom .left .select-version h2 {
        margin: 3px 10px 0 0;
    }

    #bottom .left .title {
        text-align: left;
        margin-top: 20px;
    }

    #bottom .left .menu {
        text-align: left;
        margin-top: 10px;
    }

    #bottom .right {
        width: 100%;
        display: flex;
        align-content: center;
        justify-content: center;
        margin-top: 30px;
    }

    #bottom .right .content {
        width: 40%;
        text-align: left;
    }

    /**************************************************/
    #bottom .right .content h1 {
        margin: 20px 0;
        color: #73abfe;
    }

    #bottom .right .content h2 {
        margin-bottom: 20px;
    }

    #bottom .right .content h3 {
        margin-bottom: 10px;
    }

    #bottom .right .content pre {
        background-color: #e7ecf3;
        overflow: auto;
        padding: 10px 20px;
        border-radius: 4px;
        margin: 10px 0;
    }

    #bottom .right .content img {
        width: 100%;
    }
</style>