# TimerButton
#计时按钮

* uses immediately

![image](https://github.com/NR917/TimerButton/raw/master/pic1.gif)

* some setting

![image](https://github.com/NR917/TimerButton/raw/master/pic4.gif)

Build some wheels series-TimerButton
 * 1-provide duration setting
 * -提供计时时长设置
 * 2-provide forward and reverse timing mode，default reverse mode；
 * -提供正序和逆序计时，默认逆序倒数计时
 * 3-provide timing start callback，it receive a variable of boolean type to decide whether response onClick event this time；
 * -提供计时开始回调，接收布尔值，return true则点击开始计时；return false则不开始，用于一些场景业务逻辑的判断需要，比如两次输入密码是否一致后再发送验证码
 * 4-provide timing finish callback
 * -提供计时完成回调onTimeFinish
 * 5-provide every second callback
 * -提供每一秒计时回调onEverySecond
 * 6-provide public method to control start and cancel
 * -提供开始计时和结束计时方法
 * How to use
 * -1，setTimerDuration;2,.autoMode() or .manusalMode();3,setOnEverySecondeLIstener;
 * -使用方法：1，setTimerDuration；2，autoMode（自动或手动）；3，setOnEverySecondListener；
 
#使用场景
#Use scenario
 * 1-The most simple to use, when you just need a simple timing
 * -完成简单的计时逻辑即可
 
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
 
 * 2-Logic to decide
 * -逻辑判断
 
 >Eample：if you need to decide start timing after you do something, you can uses like this
 
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
