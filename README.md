# SpannableTextView
Spanning of any string in single TextView using below code


//START
        Typeface font = Typeface.createFromAsset(getActivity().getAssets(), getResources().getString(R.string.FONT_EXTRABOLDITALIC));

        SpannableString spannable = new SpannableString("Text is\nSPANtastic!");
        spannable.setSpan(
                new CustomTypefaceSpan("", font),
                8, spannable.length(),
                Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
        spannable.setSpan(
                new ForegroundColorSpan(Color.RED),
                8, spannable.length(),
                Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);



class CustomTypefaceSpan extends TypefaceSpan {

    private final Typeface newType;

    public CustomTypefaceSpan(String family, Typeface type) {
        super(family);
        newType = type;
    }

    private static void applyCustomTypeFace(Paint paint, Typeface tf) {
        int oldStyle;
        Typeface old = paint.getTypeface();
        if (old == null) {
            oldStyle = 0;
        } else {
            oldStyle = old.getStyle();
        }

        int fake = oldStyle & ~tf.getStyle();
        if ((fake & Typeface.BOLD) != 0) {
            paint.setFakeBoldText(true);
        }

        if ((fake & Typeface.ITALIC) != 0) {
            paint.setTextSkewX(-0.25f);
        }

        paint.setTypeface(tf);
    }

    @Override
    public void updateDrawState(TextPaint ds) {
        applyCustomTypeFace(ds, newType);
    }

    @Override
    public void updateMeasureState(TextPaint paint) {
        applyCustomTypeFace(paint, newType);
    }
}

//END
