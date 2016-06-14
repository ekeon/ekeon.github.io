---
layout: post
title:  "CustomView"
date:   2015-04-10 5:43
categories: jekyll update
---
```java
public class RoundedTextView {

  private int outlineColor;
  private float outlineSize = 0f;
  private float outlineRadius = 0f;
  private int backgroundColor;
  private PaintDrawable paintDrawable;
  private PaintDrawable paintDrawable2;


  public RoundedTextView(Context context) {
    super(context);
  }

  public RoundedTextView(Context context, AttributeSet attrs) {
    super(context, attrs);
    setAttrs(context, attrs);
  }

  public RoundedTextView(Context context, AttributeSet attrs, int defStyle) {
    super(context, attrs, defStyle);
    setAttrs(context, attrs);
  }

  private void setAttrs(Context context, AttributeSet attrs) {
    TypedArray ta = context.obtainStyledAttributes(attrs, R.styleable.########);
    backgroundColor = ta.getColor(R.styleable.########);, Color.TRANSPARENT);        // textview 뒷 배경 색 (기본 투명)
    outlineColor = ta.getColor(R.styleable.########);, Color.BLACK);                    // textview 테두리 컬러 (기본 검정)
    outlineSize = ta.getFloat(R.styleable.########);, 0.5f);                          // textview 테두리 두께
    outlineRadius = ta.getFloat(R.styleable.########);, R.dimen.px35);                       // textview 테두리 둥근정도

  }

  public void setTextBackgroundColor(int color) {
    this.backgroundColor = color;
    invalidate();
  }

  public void setTextOutLineColor(int outlineColor) {
    this.outlineColor = outlineColor;
    invalidate();
  }

  public void setTextOutLineSize(float outlineSize) {
    this.outlineSize = outlineSize;
    invalidate();
  }

  public void setTextOutLineRadius(float outlineRadius) {
    this.outlineRadius = outlineRadius;
    invalidate();
  }

  @Override
  protected void onDraw(Canvas canvas) {
    if (paintDrawable == null) {
      paintDrawable = new PaintDrawable(backgroundColor);                                     // 텍스트뷰 안쪽
      paintDrawable2 = new PaintDrawable(Color.BLACK);                                        // 텍스트뷰 바깥쪽
    }

    paintDrawable.getPaint().setStyle(Paint.Style.FILL_AND_STROKE);                             // 안쪽을 채우고 스트록을줌
    paintDrawable.getPaint().setColor(backgroundColor);                                                     // 색칠
    paintDrawable.getPaint().setPathEffect(new CornerPathEffect(outlineRadius));            // 채운곳에 둥근 정도

    canvas.drawPaint(paintDrawable.getPaint());

    paintDrawable2.getPaint().setStyle(Paint.Style.STROKE);                                                   // 테두리 스타일
    paintDrawable2.getPaint().setStrokeJoin(Paint.Join.ROUND);                                             // 테두리 모양을 둥글게
    paintDrawable2.getPaint().setColor(outlineColor);                                                                 // 테두리 색
    paintDrawable2.getPaint().setStrokeWidth(outlineSize);                                                       // 테두리 두께
    paintDrawable2.getPaint().setPathEffect(new CornerPathEffect(outlineRadius));               // 테두리 둥근 정도

    paintDrawable2.getPaint().setAntiAlias(true);                                                   // 페인트를 부드럽게
    canvas.drawPaint(paintDrawable2.getPaint());                                                // 덮어씌워지는것을 방지 하기 위해 캔버스에 지정해
    super.onDraw(canvas);
  }
}

```
