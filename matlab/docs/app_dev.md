## 初始代码

```java
% 定义一个名为app1的类，继承自matlab.apps.AppBase
classdef app1 < matlab.apps.AppBase
    % 定义应用程序的属性，包括UIFigure、GridLayout和Hyperlink
    properties (Access = public)
        UIFigure    matlab.ui.Figure      % UIFigure属性
        GridLayout  matlab.ui.container.GridLayout  % GridLayout属性
        Hyperlink   matlab.ui.control.Hyperlink  % Hyperlink属性
    end
    
    % 定义组件初始化的方法
    methods (Access = private)
        % 创建UIFigure和组件的方法
        function createComponents(app)
            % 创建UIFigure并隐藏，直到所有组件创建完成
            app.UIFigure = uifigure('Visible', 'off');
            app.UIFigure.Color = [0.9216 0.7922 0.7922];  % 设置UIFigure的颜色
            app.UIFigure.Position = [100 100 827 529];  % 设置UIFigure的位置
            app.UIFigure.Name = 'MATLAB App';  % 设置UIFigure的名称
            
            % 创建GridLayout
            app.GridLayout = uigridlayout(app.UIFigure);
            app.GridLayout.ColumnWidth = {'1x', '1x', '1x', '1x'};  % 设置GridLayout的列宽
            app.GridLayout.RowHeight = {'1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x', '1x'};  % 设置GridLayout的行高
            
            % 创建Hyperlink
            app.Hyperlink = uihyperlink(app.GridLayout);
            app.Hyperlink.HorizontalAlignment = 'center';  % 设置Hyperlink的水平对齐方式
            app.Hyperlink.Layout.Row = 1;  % 设置Hyperlink的行布局
            app.Hyperlink.Layout.Column = 1;  % 设置Hyperlink的列布局
            
            % 显示UIFigure，所有组件创建完成后
            app.UIFigure.Visible = 'on';
        end
    end
    
    % 定义应用程序创建和删除的方法
    methods (Access = public)
        % 构造应用程序的方法
        function app = app1
            % 创建UIFigure和组件
            createComponents(app)
            % 将应用程序注册到App Designer
            registerApp(app, app.UIFigure)
            % 如果没有输出参数，清除app变量
            if nargout == 0
                clear app
            end
        end
        
        % 在应用程序删除前执行的代码
        function delete(app)
            % 删除UIFigure，当应用程序被删除时
            delete(app.UIFigure)
        end
    end
end
```

