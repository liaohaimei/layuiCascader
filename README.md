# layuiCascader
@Name: 基于layui的ajax异步无限级联选择器
@Author: 罗茜
创建时间: 2019/05/23
修改时间：2019/05/27 ----- 2019/05/28	----- 2019/05/29 ----- 2019/05/30
使用说明: 在主文件里面使用layui.config设置，具体方法看index.html

## 使用说明

### 一、Demo

此插件主要用来实现数据异步加载功能，具体使用方法，请参照index.html

优点：

1.已获取的数据不再重复获取

2.回显功能只需一个参数即可

![demo](E:\开源项目\layuiCascader\assets\demo.png)

### 二、定义配置项options

```
let options={           	
    elem:'#demo'                              //【必填】dom对应的id值或class值，最好为id
    ,width:100                                //【可选】input框宽度  【默认：220】  
    ,height:50                                //【可选】input框高度  【默认：40】
    ,prop:{
         value:'value',                       //【可选】定义接口需要取得的值的名称字段【默认:value】
         label:'label',                       //【可选】定义接口显示的名称字段  【默认：label】
         children:'children'                  //【可选】定义接口子集的名称字段 【默认：children】
    }
    ,showlast:false                           //【可选】是否只显示最后一级 【默认：false】
    
    ,data:[]                                  //【二选一】初始化的值
    ,value:0                                  //【二选一】ajax请求初始值,即获取根结点的初始请求参数

    ,getChildren:function(value){             //【可选】用户自定义获取data子集的方法,
        let data = [];               //  value为当前dom的value值
        $.ajax({                         
            url:'https://open.gog.cn/appz/region/getRegion/'+value,
            type:'get',
            async:false,
            success:(res)=>{
                data = res.data;
                for(let i in data){
                    data[i].value = data[i].id;
                    data[i].label = data[i].name;
                    delete data[i].id;
                    delete data[i].name;
                    data[i].hasChild = true;
                }
            }
        });
        return data;
    }
    ,checkData:['520000000000','520300000000','520302000000']  //回显参数               
}
```

## 三、初始化Cascader

```
cascader.load(options);
```

## 四、方法

```
cascader.getChooseData()						
// 其返回值用一个变量存储即可
// 返回类型：数组
// 返回元素：所有已选择的value值
// ['520000000000','520300000000','520302000000']
```

```
// 选择器点击事件的监听
cascader.on('click',function(){
	
});
// 选择器hover事件的监听
cascader.on('hover',function(){
	
});
```

