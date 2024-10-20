## 登陆界面
#### 组件：   
```
UIFigure    matlab.ui.Figure
Label_2     matlab.ui.control.Label
TextArea_2  matlab.ui.control.TextArea
TextArea    matlab.ui.control.TextArea
Label       matlab.ui.control.Label
Button_3    matlab.ui.control.Button
Image       matlab.ui.control.Image
```


#### 回调函数：
```java
        % Button pushed function: Button_3
        function Button_3Pushed2(app, event)
        username = char(app.TextArea.Value);
        password = char(app.TextArea_2.Value);

    % 设置逻辑
        if strcmp(username, '123') && strcmp(password, '123')
            msgbox("登陆成功")
            delete(app.UIFigure);
        else
            msgbox("账号密码错误");
        end

        end    
```        

