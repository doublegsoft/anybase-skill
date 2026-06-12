Skill: modelbase
================

## 命名规范

### 对象、字段命名

要求在英文语义环境中正确表达对象、字段实际意义。

### 持久化对象命名

* 实体对象的定义：只有一个标识字段的我们称之为实体对象。它的持久化名称以tn开头，第二部分是模块名称的缩写，第三部分是对象名称的缩写。

  ```
  @persistence(name='tn_pm_proj')
  project<
  
    @persistence(name='projid'>
    id!!: long,
    
    ...
  >
  ```
  
* 值体对象的定义：有两个及以上的标识字段的对象，并且它其中一个或多个标识字段是引用了其他对象，我们称之为值体对象。 它的持久化名称以tv开头，第二部分是模块名称的缩写，第三部分是对象名称的缩写。

  ```
  @persistence(name='tv_pm_projmem')
  project_member<
  
    @persistence(name='projid'>
    project!!: &project(id),

    @persistence(name='memid'>
    member!!: &employee(id),

    ...
  >
  ```
  
* 连接对象的定义：有两个及以上的标识字段的对象，并且它其中一个或多个标识字段是引用了其他对象，而且除了标识字段以外没有其他业务字段，我们称之为连接对象。 它的持久化名称以tx开头，第二部分是模块名称的缩写，第三部分是对象名称的缩写。

  ```
  @persistence(name='tx_hrm_emplrol')
  employee_role<
  
    @persistence(name='emplid'>
    employee!!: &employee(id),
  
    @persistence(name='rolid'>
    role!!: &role(id),

    ...
  >
  ```
  
* 常量对象的定义：通常是数据字典，我们称之为常量对象。它的持久化名称以tc开头，第二部分是模块名称的缩写，第三部分是对象名称的缩写。


  ```
  @persistence(name='tc_hrm_pos')
  position<
  
    @persistence(name='posid'>
    id!!: long,
  
    ...
  >
  ```  


### 持久化字段命名

持久化字段命名有一套简单的公式：

* 首先，构成字段的单词，每一个单词的缩写加在一起构成持久化字段名。比如：
  
  ```
  @persistence(name='projsts')
  project_status: enum[IN:INITIAL('开始'), CP:COMPLETED('完成')]
  ```
  project的缩写proj, status的缩写sts，这两个单词的缩写组合在一起，就构成了持久化字段名projsts。
  
* 如果属性名称是id、name、type、code、group这几个属性，持久化名称需要加上对象名称的缩写。比如：
  
  ```
  @persistence(name='projmsgid')
  id!!: long
  ```
  这个字段是project_message的标识字段，对象名称是project_message，所以它的持久化名称就是proj + msg + id = projmsgid。
  
  ```
  @persistence(name='projmsgnm')
  name!!: long
  ```
  这个字段是project_message的字段，对象名称是project_message，name的缩写是nm，所以它的持久化名称就是proj + msg + nm = projmsgnm。
  
### 易出错的字段类型

* 日期、时间、时间戳都用**datetime**类型。
* 可以有小数位的数字用**number**类型，通常为**number(12,4)**，12是总共长度，4是小数位数
* 主键用**long**类型

### 其他要求

* 对象和属性都要加上**@name**，并且需要加上合理的plural和singular。

  ```
  @persistence(name='tn_pm_proj')
  @name(label='项目', plural='projects')
  project<
  
    @persistence(name='projid'>
    @name(label='项目标识')
    id!!: long,
    
    @name(label='项目成员', singular='member')
    @conjunction(object='project_member')
    members: &employee(id)[],
    ...
  >

  ```
