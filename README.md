# TimerButton


* uses 

![image](https://github.com/NR917/TimerButton/raw/master/pic1.gif)

* setting

![image](https://github.com/NR917/TimerButton/raw/master/pic4.gif)

Build some wheels series-TimerButton
 * -提供计时时长设置
 * -提供正序和逆序计时，默认逆序倒数计时
 * -提供计时开始回调，接收布尔值，return true则点击开始计时；return false则不开始，用于一些场景业务逻辑的判断需要，比如两次输入密码是否一致后再发送验证码
 * -提供计时完成回调onTimeFinish
 * -提供每一秒计时回调onEverySecond
 * -提供开始计时和结束计时方法
 * 如何使用
 * -1，setTimerDuration;2,.autoMode() or .manusalMode();3,setOnEverySecondeLIstener;
 * -使用方法：1，setTimerDuration；2，autoMode（自动或手动）；3，setOnEverySecondListener；
 
 
 <pre><code>
 btn = (TimerButton) findViewById(R.id.btn);
 btn.setTimerDuration(30);
        btn.setOnEverySecondListener(new TimerButton.OnEverySecondListener() {
            @Override
            public boolean onTimingStart() {
                btn.setText("Retry After " + 10 + " Second");
                return true;
            }

            @Override
            public void onEverySecond(int seconde) {
                btn.setText("Retry After " + seconde + " Second");
            }

            @Override
            public void onTimingFinish() {
                btn.setText("Start");
            }
        });
 </code></pre>
 
 * -逻辑判断
 
 >Eample：
 
 <pre><code>
 btn = (TimerButton) findViewById(R.id.btn);
        btn.setTimerDuration(30);
        btn.manualMode();//for control the timing you need to set this mode
        btn.setOnEverySecondListener(new TimerButton.OnEverySecondListener() {
            @Override
            public boolean onTimingStart() {
                btn.setText("Retry After " + 10 + " Second");
                //do something(example:a Asynchronous task, 
                // when the callback response, you can uses btn.go() in the runOnUiThread() to start timing)

                return true;
            }

            @Override
            public void onEverySecond(int seconde) {
                btn.setText("Retry After " + seconde + " Second");
            }

            @Override
            public void onTimingFinish() {
                btn.setText("Start");
            }
            });
 </code></pre>
 
 >like this
 
 <pre><code>
 //for example when my callback response i call the .go() method in runOnUiThread() to start timing
            @Override
            public void onSuccess(JSONObject response) {
                
                try {
                    if (response.getString(ApiHelper.HTTP_REQUEST_RESULT_CODE).equals(ApiHelper.HTTP_REQUEST_RESULT_OK)) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                btnGetcode.go();
                                btnGetcode.setText(sec + "秒后重试");
                            }
 </code></pre>
 
#Please enjoy~!Hope this wheel bring you help!
