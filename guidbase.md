Skill: guidbase
================

## 元素类型

### 基础编辑类型

* **text** 文本 
* **date** 日期 
* **time** 时间 
* **select** 单选 
* **multiselect** 多选 
* **cascade** 层级 
* **tagsinput** 标签 
* **avatar** 头像，通常为圆形图片的展示。
* **longtext** 长文本 

### 容器类型

* **page** 页面，每个页面都有这个根对象

  ```
  project_list_page:page(title: "项目信息")<
    ...
  >
  ```
  
* **tabs** 分页标签，子元素是tab

  ```
  project_tabs:tabs(title: "项目信息")<
    base_tab:tab(title: "基本信息")<
      ...
    >
    ...
  >
  ```  

* **entry_form** 编辑表单，用于信息编辑

  ```
  project_form:entry_form(title: "项目信息", object: "project", cols: "3")<
    project_name:text(title:"项目名称"),
    ...
  >
  ```
  
* **excel_form** 广义表单，类似于excel一样编辑集合数据

  ```
  project_member_table:excel_form(ttile:"项目成员", object: "project_member")<
    member_name:text(title:"姓名"),
    role:select(title:"角色"),
    ...
  >
  ```
* **criteria_form** 条件表单，输入查询条件的表单

  ```
  project_member_criteria:criteria_form(ttile:"项目成员", object: "project_member")<
    member_name:text(title:"姓名"),
    role:select(title:"角色"),
    ...
  >
  ```  

* **display_form** 只读表单，用于信息展示

  ```
  project_form:display_form(title: "项目信息", object: "project")<
    project_name:text(title:"项目名称"),
    ...
  >
  ```
  
* **paged_table** 分页表格，用于集合信息展示

  ```
  project_table:paged_table(ttile:"项目列表", object: "project")<
    project_name:text(title:"项目名称"),
    start_date:date(title:"开始时间"),
    ...
  >
  ```
  
## 属性解释

* **id**:**type** 标识id和类型，通常在页面中每个元素都指定一个id
* **title** 标题，每个元素都应该有
* **object** 引用的数据对象，在modelbase中定义的对象
* **ref** 在页面中引用的其他元素，比如保存按钮需要引用到具体保存那个表单
* **cols** 这个跟布局有关，就是元素分成几列，通常用于容器类型
* **span** 这个跟布局有关，指元素在容器的布局中占用几列
* **size** 大小，格式为：(100,200)，即宽度100，高度200，单位都是px
* **viewport** 视图区域，通常信息浏览的打开方式是drawer，信息编辑的打开方式是dialog，有集合元素通常都需要这些元素。

## 其他要求

* 多个元素之间必须要有comma符号分割，最后一个不需要。
* 每个页面都要有**module**属性，属性值是英文缩写，外部有对应关系
