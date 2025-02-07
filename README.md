<!DOCTYPE html>
<html lang="zh-cmn-Hans">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <title>校外人员入校登记</title>
    <link href="https://yqsb.qau.edu.cn/assets/css/frontend.css?v=1591683153" rel="stylesheet">
    <style>
      .weui-btn {
        display: block;
        position: relative;
        padding: 0 14px;
        box-sizing: border-box;
        font-size: 18px;
        color: #fff;
        line-height: 2.55555556;
        border-radius: 5px;
        text-decoration: none;
        -webkit-tap-highlight-color: transparent;
        margin: 0 10px
      }

      .weui-btn_success {
        background-color: #1aad19
      }

      .weui-btn_disabled {
        color: rgba(255, 255, 255, .6)
      }

      .weui-btn_mini {
        display: inline-block;
        padding: 0 1.32em;
        line-height: 2.3;
        font-size: 13px
      }

      .weui-cells {
        margin-top: 1.17647059em;
        line-height: 1.47058824;
        font-size: 17px;
        position: relative
      }

      .weui-cells__title {
        margin-top: .77em;
        margin-bottom: .3em;
        padding-left: 15px;
        padding-right: 15px;
        color: #000;
        font-size: 17px
      }

      .weui-cell {
        padding: 10px 15px;
        display: flex;
        align-items: center;
        position: relative
      }

      .weui-cell__bd {
        flex: 1
      }

      .weui-input {
        width: 100%;
        border: 0;
        outline: 0;
        -webkit-appearance: none;
        background-color: transparent;
        font-size: inherit;
        color: inherit;
        height: 1.47058824em;
        line-height: 1.47058824
      }

      .weui-dialog {
        position: fixed;
        width: 80%;
        max-width: 300px;
        left: 50%;
        background-color: #fff;
        border-radius: 3px;
        text-align: center;
        transform: translate(-50%, -50%);
        top: 45%;
        z-index: 2000
      }

      .weui-dialog__hd {
        padding: 1.3em 1.6em .5em
      }

      .weui-dialog__title {
        font-weight: 400;
        font-size: 18px
      }

      .weui-dialog__bd {
        padding: 0 1.6em .8em;
        min-height: 40px;
        font-size: 15px;
        line-height: 1.3;
        word-wrap: break-word;
        word-break: break-all;
        color: #999;
        text-align: left
      }

      .weui-mask {
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        background: rgba(0, 0, 0, .6);
        z-index: 1000
      }

      .weui-dialog.weui-dialog--visible,
      .weui-mask.weui-mask--visible {
        opacity: 1;
        visibility: visible
      }

      .page {
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        overflow-y: auto;
        background-color: #f8f8f8;
        z-index: 1
      }

      .navbar-inverse {
        margin-bottom: 0;
        color: #fff;
        text-align: center;
        font-size: 18px;
        line-height: 50px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap
      }

      #check-alert {
        color: #000;
        font-size: 16px;
        font-weight: 700
      }

      #gg-timer {
        color: #8b0000
      }

      #check-success-title {
        font-weight: 700;
        color: #0a6332;
        font-size: 20px
      }

      ::-webkit-scrollbar {
        display: none
      }

      .page {
        position: absolute;
        top: 10px;
        right: 0;
        bottom: 0;
        left: 0;
        overflow-y: auto;
        background-color: #f8f8f8;
        z-index: 1
      }
    </style>
    <script>
      function formatDate(date) {
        return date.getFullYear() + '-' + String(date.getMonth() + 1).padStart(2, '0') + '-' + String(date.getDate()).padStart(2, '0')
      }

      function updateAccessPeriod() {
        const now = new Date();
        const startDate = new Date(now);
        const endDate = new Date(now);
        endDate.setDate(endDate.getDate() + 30);
        document.getElementById('accessPeriod').textContent = formatDate(startDate) + ' ~ ' + formatDate(endDate)
      }

      function updateTimer() {
        const now = new Date();
        const formattedTime = now.getFullYear() + '-' + String(now.getMonth() + 1).padStart(2, '0') + '-' + String(now.getDate()).padStart(2, '0') + ' ' + String(now.getHours()).padStart(2, '0') + ':' + String(now.getMinutes()).padStart(2, '0') + ':' + String(now.getSeconds()).padStart(2, '0');
        document.getElementById('gg-timer').textContent = formattedTime
      }
      window.onload = function() {
        updateAccessPeriod();
        setInterval(updateTimer, 1000)
      };
    </script>
  </head>
  <body>
    <nav class="navbar navbar-inverse navbar-fixed-top fix-width bg-red" role="navigation"> 校外人员入校登记 </nav>
    <div class="page" style="margin-top: 25px">
      <div class="weui-cells weui-cells_form">
        <div class="weui-cells__title" id="tel_lable">手机号</div>
        <div class="weui-cell">
          <div class="weui-cell__bd">
            <input class="weui-input" type="tel" name="row[tel]" id="tel" required="" pattern="[0-9]{11}" maxlength="11" placeholder="13573869748">
          </div>
        </div>
        <div style="margin-top: 15px;text-align: center">
          <button id="formSubmitBtn" type="button" class="weui-btn weui-btn_mini weui-btn_success weui-btn_disabled" disabled="disabled">提交</button>
        </div>
      </div>
    </div>
    <div class="weui-mask weui-mask--visible"></div>
    <div class="weui-dialog weui-dialog--visible">
      <div class="weui-dialog__hd">
        <strong class="weui-dialog__title">
          <span id="check-success-title" style="font-weight: bold;color: #0a6332;font-size: 20px">允许通行</span>
        </strong>
      </div>
      <div class="weui-dialog__bd">
        <div id="check-alert">
          <p>陈亚铎&nbsp;您好:</p>
          <p>您的申请已通过，允许您正常出入</p>
          <p>通行日期： <span id="accessPeriod">2024-12-22 ~ 2025-01-21</span>
          </p>
          <p>当前时间： <span id="gg-timer">2025-1-6&nbsp; 19:13:12</span>
          </p>
        </div>
      </div>
    </div>
  </body>
</html>
