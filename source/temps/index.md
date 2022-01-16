---
title: 活动案例
date: 2022-01-06 21:52:55
---

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
<style>
    .container{
        margin:0px auto 20px;
    }
    .preview{
        text-decoration:none;
        color:#313131;
    }
    .sidebar{
        position: fixed;
        z-index: 9;
        left: -8rem;
        bottom: 0;
        width: 8rem;
        height: 100%;
        background-color: rgba(0,0,0,.8);
    }
    .navbar .nav .nav-item-link {
        display: block;
        padding: 1rem;
        color: #bbb;
        text-decoration: none;
        cursor: pointer;
    }
    .navbar-bottom {
        position: absolute;
        bottom: 0;
        width: 100%;
        font-size: 2rem;
    }
    .navbar{
        display:block;
        position: relative;
        padding-top: 3rem;
        text-align: center;
    }
    .nav{
        display:block;
        list-style: none;
        padding-left: 0;
        margin-left: 0;
    }
    .temp-item{
        width: 205px;
        padding: 10px 0;
        margin: 10px auto;    
        border-radius: 18px;
        background: #f4f4f4;
        box-shadow:  3px 3px 6px #bebebe, 
                    -3px -3px 6px #ffffff;
    }
    .temp-item:hover{
        box-shadow: inset -6px -6px 20px rgba(255,255,255,0.7), inset 6px 6px 20px rgba(0,0,0,0.08);
    }
    .temp-item-content{
        padding:8px;
        height: 34px;
    }
    .temp-item-content h4{
        margin: 0.5rem;
    }
    .temp-item-content .play{
        position: relative;
        top: -24px;
        left: 155px;
        border-radius: 104px;
        background: #f9f9f9;
        padding: 5px;
        box-shadow: -6px -6px 20px rgb(255 255 255), 6px 6px 20px rgb(0 0 0 / 10%);
    }
    .ifr{
        display: table;
        border-radius:8px;
    }
</style>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>

<div class="container" >
    <h3><a href="#98" class="headerlink" title="98%"></a>98%</h3>
    <div id="98%" class="row row-cols-sm-1 row-cols-md-3">
    </div>
    <h3><a href="#Mr-Kwon" class="headerlink" title="Mr.Kwon"></a>Mr.Kwon</h3><div style="display: flex;"></div>
    <div id="MrKwon" class="row row-cols-sm-1 row-cols-md-3">
    </div>
</div>

<script>
    var config = {
        "98%":[{"name":"FlappyBird",link:"https://www.aichaos.cn/98Percent/FlappyBird/released/index.html"}],
        "MrKwon":[
            {"name":"2048 合成",link:"https://www.aichaos.cn/MrKwon/released/index.html?game=2048"},
            {"name":"六边形消除",link:"https://www.aichaos.cn/MrKwon/released/index.html?game=hextris"},
            {"name":"五子棋",link:"https://www.aichaos.cn/MrKwon/released/index.html?game=gobang"}
        ]
    }

    var keys = Object.keys(config)
    keys.forEach(key=>{
        if(config[key] && config[key].length>0){
            var child = ""
            config[key].forEach(item=>{
                var temp = `
                    <div class="col">
                        <div class="temp-item">
                            <iframe class="ifr m-auto" height=301.5 width=187.5 src="${item.link}" frameborder=0  ></iframe>
                            <a class="preview" href="https://www.aichaos.cn/preview/?purl=${encodeURIComponent(item.link)}">
                            <div class="temp-item-content">
                                <h4>${item.name}</h4>
                                <span class="play">▶</span>
                            </div>
                            </a>
                        </div>
                    </div>
                `
                child+=temp
            })
            console.log(child)
            document.getElementById(key).innerHTML = child
        }
        
    })
</script>