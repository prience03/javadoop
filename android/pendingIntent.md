```java
//    打开activity
//    */
    //打开activity按钮不带参数
    //        PendingIntent Pfullintent = PendingIntent.getActivity(context, 0, fullIntent, 0);
    //打开activity按钮带参数
    //        PendingIntent Pfullintent = PendingIntent.getActivity(context, 0, fullIntent, PendingIntent.FLAG_CANCEL_CURRENT);
    /*
      打开service
        */
//    Intent serviceIntent = new Intent(context, MyService.class);
//    PendingIntent servicePendingIntent = PendingIntent.getService(context, 0, serviceIntent, 0);
//    views.setOnClickPendingIntent(R.id.appwidget_service_btn, servicePendingIntent);
    /*
      发送action
        */
//    Intent anIntent = new Intent("com.action.haha");
//    PendingIntent anPendingIntent = PendingIntent.getBroadcast(context, 0, anIntent, 0);
//    views.setOnClickPendingIntent(R.id.appwidget_brocast_btn, anPendingIntent);
```