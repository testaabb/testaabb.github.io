---
layout: post
title: Android之旅（四） -- Intent
category: Android
tags: [Android]
excerpt: >
  Intent传值：
---

Intent传值：
注意：
        被传递的类要implement Serializable
        不能传Bitmap
实现：
        CurrentActivity类中

        ```java
        Intent intent = new Intent(CurrentActivity.this, ResultActivity.class);
        Bundle bundle = new Bundle();
        intent.putSerializable("标记key", 被传递对象的实例);
        intent.putExtras(bundle);
        startActivity(intent);
        ```

        ResultActivity类中
        ```java
        被传递对象的实例 = (被传对象)getIntent.getSerialzable("key");
        ```