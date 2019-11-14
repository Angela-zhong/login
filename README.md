# 项目介绍
利用bootstrap模态框使用 iframe标签使用 label标签for属性使用.........................
# 登录功能业务逻辑
<script>
    //入口函数
    $(function () {
      /* 登录功能思路
      1.给登录按钮注册点击事件
      2.阻止默认跳转事件（表单submit会自动跳转页面）
      3.获取用户名和密码
      4.非空判断
      5.ajax发送请求
      6.处理响应结果   a.成功：跳转管理系统首页    b.失败：提示用户
       */
      //1.给登录按钮注册点击事件
      $('.input_sub').click(function (e) {
        //2.阻止默认跳转事件（表单submit会自动跳转页面）
        e.preventDefault();
        //3.获取用户名和密码
        var username = $('.input_txt').val().trim();//去除前后空格
        var password = $('.input_pass').val().trim();
        //4.非空判断
        if (username == '' || password == '') {
          alert('用户名与密码不能为空');
          return;
        };
        //5.ajax发送请求
        $.ajax({
          url: 'http://localhost:8080/api/v1/admin/user/login',
          type: 'post',
          dataType: 'json',
          data: {
            username,
            password
          },
          success: function (backData) {
            console.log(backData);
            //6.处理响应结果  a.成功：跳转管理系统首页  b.失败：提示用户
            if(backData.code == 200){
              //跳转首页
              window.location.href = './index.html';
            }else{
              alert(backData.msg);
            }
          }
        });  
      });
    });
  </script>
