# settings
## www/mvc_settings.lua
这个文件将在框架加载的时候自动被执行，并且是在模块被加载之前。
### 示例
```lua
local nwf = commonlib.gettable("nwf");
local config = commonlib.gettable("nwf.config");

config.echoDebugInfo = true;  -- 是否在页面上显示调试信息

-- nwf模块项目的模块basedir相对与本项目的根目录的路径
local moduleSearchPath = '../nwfModules/nwf_modules/';
-- 把功能模块项目加入模块搜索路径，且优先于项目内安装的模块（用于调试模块）。
table.insert(nwf.mod_path, 1, moduleSearchPath);
```
### 可以设置的配置项

| 配置项名           | 值 | 值的类型 | 描述信息 |
| ------------------- | ------------------ | ------------ |------------ |
| nwf.config.echoDebugInfo | true/false | boolean | 如果设置为true则表示将直接在网页中输出调试信息 |
| nwf.config.redirectToErrorPage | true/false | boolean | 指示是否在发生错误时跳转到错误页（该配置项仅当nwf.config.echoDebugInfo设置为false时有效）|
| nwf.mod_path | 模块搜索路径 | 字符串数组 | 这是一个相对于项目根目录的相对路径组成的数组，网站启动时将会根据这些指定的路径去加载模块。在数组中越靠前的路径，搜索时优先级越高。|
| nwf.config.session_cookie_key | session id key | 字符串 | session id将会保存在cookie中，本配置项指定cookie的key。 |
| nwf.config.session_timeout | session timeout seconds | 整型数 | 指定session超时的秒数 |

## www/app_initialized.lua
这个文件将会在框架完全加载完毕并且服务器启动之后执行，你可以在这个文件中加入应用启动之后需要执行的代码。  
### e.g.
```lua
------------------------------------------------------------------
--      desc: 服务器、框架完全加载之后的处理脚本
--      author: zenghui
--      date: 2017-3-27
--      attention: 网站启动时将自动执行此文件一次。
--      注意此文件执行之时服务器、框架、模块已经完全加载完毕。
--      可以在这个文件里加入一些业务脚本
------------------------------------------------------------------
local nwf = commonlib.gettable("nwf");

------------------------------------------------------------------
--  这里加载web应用需要的公共模块
--	e.g. NPL.load("(gl)www/utils/stlutil.lua");
------------------------------------------------------------------


------------------------------------------------------------------
--  这里注册web应用的各种过滤器
------------------------------------------------------------------

--[[
    nwf.registerFilter(function(ctx, doNext)
        local req = ctx.request;
        local res = ctx.response;
        doSomething();
        doNext();
        doSomething();
    end);
]]

------------------------------------------------------------------
--  这里加载业务组件
--	e.g. NPL.load("(gl)www/service/xxx.lua");
------------------------------------------------------------------


------------------------------------------------------------------
--  网站启动成功的提示信息
------------------------------------------------------------------
print("nwf application starting completed.");

```
