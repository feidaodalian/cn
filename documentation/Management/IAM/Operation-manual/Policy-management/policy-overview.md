# 策略管理

京东云权限策略，是一种对京东云访问权限的描述语言。本文将介绍京东云权限策略的定义和分类。

## 策略定义

策略是定义IAM用户权限的对象。撰写策略需要遵循 JSON 语法规范。

通过给子用户/群组/角色附加策略，来使子用户/群组/角色拥有策略所定义的权限。

IAM 支持两种类型的策略：京东云预置的系统策略和用户自行管理的自定义策略。

## 策略类型

京东智联云目前支持两种类型的策略：

- 托管策略
- 会话策略

### 托管策略

托管策略是附加到 IAM 身份的策略，根据托管者的不同又可细分为系统策略和自定义策略。

其中，系统策略是京东智联云托管的策略，由京东智联云创建和管理，用户不可修改或删除。系统策略因无法指定具体的 JRN（京东智联云资源唯一标识），因此提供对某产品线资源的完全访问权限。如 JDCloudVirtualMachineAdmin 策略支持管理用户账号下的所有云主机资源。

自定义策略为用户托管的策略，由用户自行创建和管理。自定义策略可以通过指定资源（Resource）或指定条件键（Condition）来实现允许或拒绝对特定资源的特定操作。

### 会话策略

代入角色时所传入的策略称之为会话策略，用于限制角色会话期间的所实际拥有的权限。角色会话期间实际拥有的权限为其会话策略和附加的托管策略的交集。

会话策略随角色会话的失效而失效。

## 策略语法介绍

授权策略是一端 JSON 格式的代码，通过这段代码描述了授权策略版本、授权操作类型、授权操作对象、授权操作条件等多个内容。

策略语法的详细介绍，请参考[策略元素](../../../../../documentation/Management/IAM/Operation-manual/Policy-management/policy-grammar/elements.md)和[策略变量](../../../../../documentation/Management/IAM/Operation-manual/Policy-management/policy-grammar/variable.md)说明。

## 常用操作

[通过可视化策略生成器创建策略](../../../../../documentation/Management/IAM/Operation-manual/Policy-management/policy-manage/UI-create.md)

[通过策略编辑器创建策略](../../../../../documentation/Management/IAM/Operation-manual/Policy-management/policy-manage/Json-create.md)

[按标签创建策略](../../../../../documentation/Management/IAM/Operation-manual/Policy-management/policy-manage/Tag-create.md)

[编辑策略](../../../../../documentation/Management/IAM/Operation-manual/Policy-management/policy-manage/edit.md)

[删除策略](../../../../../documentation/Management/IAM/Operation-manual/Policy-management/policy-manage/delete.md)

