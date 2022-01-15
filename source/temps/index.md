---
title: 活动案例
date: 2022-01-06 21:52:55
---

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>

<div class="container" >
    <h3><a href="#98" class="headerlink" title="98%"></a>98%</h3>
    <div id="98%" class="row row-sm-3">
    </div>
    <h3><a href="#Mr-Kwon" class="headerlink" title="Mr.Kwon"></a>Mr.Kwon</h3><div style="display: flex;"></div>
    <div id="MrKwon" class="row row-sm-3">
    </div>
</div>

<script>
    var config = {
        "98%":[{"name":"FlappyBird",link:"https://www.aichaos.cn/98Percent/FlappyBird/released"}],
        "MrKwon":[
            {"name":"2048 合成",link:"https://www.aichaos.cn/MrKwon/released?game=2048"},
            {"name":"六边形消除",link:"https://www.aichaos.cn/MrKwon/released?game=hextris"},
            {"name":"五子棋",link:"https://www.aichaos.cn/MrKwon/released?game=gobang"}
        ]
    }

    var keys = Object.keys(config)
    keys.forEach(key=>{
        if(config[key] && config[key].length>0){
            var child = ""
            config[key].forEach(item=>{
                var temp = `
                    <div class="col">
                        <iframe  
                        height=301.5 
                        width=187.5
                        src="${item.link}"  
                        frameborder=0  
                        >
                        </iframe>
                        <a href="https://www.aichaos.cn/preview/?purl=${encodeURIComponent(item.link)}">${item.name}</a>
                    </div>
                `
                child+=temp
            })
            console.log(child)
            document.getElementById(key).innerHTML = child
        }
        
    })
</script>