---
layout: post
title:  "Android Animator!"
date:   2016-02-19 4:38
categories: jekyll update
---

간단한 안드로이드 애니메이션.
bind는 <a gref="https://github.com/JakeWharton/butterknife">버터나이프</a> 를 이용했습니다.

```java
  @Bind(R.id.imageview) ImageView imageview;
  private boolean fabUp = false;

  @OnClick(R.id.btn_hello)
  void onbtnClick() {
    ViewPropertyAnimator viewPropertyAnimator = imageview.animate();

    if (!imageviewUp) {
      imageviewUp = true;
      viewPropertyAnimator.cancel(); // 애니메이션이 취소될 경우 cancel 을 해주어어야 부드럽게 넘어감.
      viewPropertyAnimator
              .setDuration(3000)// 듀레이션설정
              .translationY(-2000)
              .rotationY(300);
      viewPropertyAnimator.start();
    } else {
      imageviewUp = false;
      viewPropertyAnimator.cancel();
      viewPropertyAnimator
              .setDuration(3000)
              .translationY(0)
              .rotationY(0);
      viewPropertyAnimator.start();
    }
  }
```

<a href="http://developer.android.com/intl/ko/reference/android/animation/Animator.html">Animator 참고문</a>

