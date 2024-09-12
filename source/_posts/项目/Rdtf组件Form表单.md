---
title: Rdtf组件Form表单
tags: Rtdf
categories: Rtdf模板
cover: /images/Rdtf组件Form表单/cover.webp
abbrlink: 8c780ec5
date: 2024-08-21 09:00:00
---

---

## Form表单

为了实现低代码量快速开发，Rdtf组件库基于Mantine封装了Form表单，通过配置confing下的index.tsx文件，即可构建你所需要的表单。


## 基本用法

配置formConfig，即可快速构建表单，当前表单支持5种类型供大家使用,如下述的一个表单配置

> 注意：表单配置中，key为必填项，label为非必填项，label为空时，key将作为label使用

```ts

export const formConfig = {
  maintenanceForm: {
    title: "账号申请",   //表单标题
    fields: [
      {
        key: "email",   //键名
        label: "邮箱",  //标签
        type: "text",  //类型
      },
      {
        key: "password",
        label: "密码",
        type: "password",
      },
      {
        key: "img",
        label: "身份证照片",
        type: "file",
      },
      {
        key: "age",
        label: "年龄",
        type: "number",
      },
      {
        key: "termsOfService",
        label: "I agree to sell my privacy",
        type: "checkbox",
      },
    ],
  },
};

```
然后在你需要的地方使用该配置即可，但你仍需了解 Mantine组件Form表单 的一些基本语法并进行相应的配置

> 注意:此处大家需自己配置form如email和termsOfService校验，并且配置提交触发的回调函数fn,具体配置可参考[Mantine官网](https://mantine.dev/form/use-form/)

```tsx

"use client";

import Form from "@/components/client/form";
import { formConfig } from "@/config";
import { useForm } from "@mantine/form";
interface Filedls {
  email: string;
  password: string;
  age: number;
  img: File | null;
  termsOfService: boolean;
}

export default function Page(props: any) {
  const form = useForm<Filedls>({
    mode: "uncontrolled",
    initialValues: {
      email: "",
      password: "",
      age: 0,
      img: null,
      termsOfService: false,
    },
    validate: {
      email: (value) => (/^\S+@\S+$/.test(value) ? null : "请输入正确的邮箱"),
      termsOfService: (value) => (value ? null : "请同意服务条款"),
    },
  });
  const fn = (v: Filedls) => {
    console.log(v);
  };

  return (
    <div>
      <Form form_config={formConfig.maintenanceForm} form={form} fn={fn} />
    </div>
  );
}


```


---