# 毕业旅记

<!--more-->
</br>
</br>
毕业旅行是为期8天的青甘环线，旅途一路所见所闻值得一记。

### 路线
<link href="https://api.mapbox.com/mapbox-gl-js/v2.6.1/mapbox-gl.css" rel="stylesheet">
<script src="https://api.mapbox.com/mapbox-gl-js/v2.6.1/mapbox-gl.js"></script>
<div id='map' style='width: 100%; height: 40rem;'></div>
<!--https://api.mapbox.com/styles/v1/mapbox/streets-zh-v1/sprite?access_token=pk.eyJ1IjoiZGlsbG9uenEiLCJhIjoiY2s2czd2M2x3MDA0NjNmcGxmcjVrZmc2cyJ9.aSjv2BNuZUfARvxRYjSVZQ
https://api.mapbox.com/styles/v1/mapbox/streets-zh-v1/sprite.png?access_token=pk.eyJ1IjoiZGlsbG9uenEiLCJhIjoiY2s2czd2M2x3MDA0NjNmcGxmcjVrZmc2cyJ9.aSjv2BNuZUfARvxRYjSVZQ -->
<script>
  mapboxgl.accessToken = 'pk.eyJ1IjoiZGlsbG9uenEiLCJhIjoiY2s2czd2M2x3MDA0NjNmcGxmcjVrZmc2cyJ9.aSjv2BNuZUfARvxRYjSVZQ';
    const map = new mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/mapbox/streets-zh-v1',
        center: [98.00000, 38.40000],
        zoom: 6
    });
    map.addControl(new mapboxgl.FullscreenControl());
    // Add zoom and rotation controls to the map.
    //map.addControl(new mapboxgl.NavigationControl({position: 'top-left'}));
    const nav = new mapboxgl.NavigationControl();
    map.addControl(nav, 'bottom-right');
    map.addControl(
    new mapboxgl.GeolocateControl({
    positionOptions: {
    enableHighAccuracy: true
    },
    // When active the map will receive updates to the device's location as it changes.
    trackUserLocation: true,
    // Draw an arrow next to the location dot to indicate which direction the device is heading.
    showUserHeading: true
    }),'bottom-right'
    );
    const scale = new mapboxgl.ScaleControl();
    map.addControl(scale, 'bottom-left');
        map.on('load', () => {
        map.addSource('route', {
            'type': 'geojson',
            lineMetrics: true,
            'data': '../static/july_trip.geojson'//'https://fastly.jsdelivr.net/gh/Lucas-0/Lucas-0.github.io/static/july_trip.geojson'
        });
        map.addLayer({
            'id': 'line',
            'type': 'line',
            'source': 'route',
            'layout': {
            'line-join': 'round',
            'line-cap': 'round'
            },
            'paint': {
            'line-color': '#86C166',
            'line-width': 5,
            'line-opacity': 0.8,
            'line-gradient': [
                'interpolate',
                ['linear'],
                ['line-progress'],
                0,
                'blue',
                0.1,
                'royalblue',
                0.3,
                'cyan',
                0.5,
                'lime',
                0.7,
                'yellow',
                1,
                'red'
                ]
            //'line-gap-width':2
            },
            'filter': ['==', '$type', 'LineString']
        });
        map.addLayer({
            'id': 'spot',
            'type': 'circle',
            'source': 'route',
            'paint': {
                'circle-radius': {
                'base': 6,
                'stops': [
                [12, 6],
                [22, 40]
                ]
                },
                'circle-color': '#C1328E'
            },
            'filter': ['==', '$type', 'Point']
        });
    map.addLayer({
            'id': 'name',
            'type': 'symbol',
            'source': 'route',
            'layout': {
          // These icons are a part of the Mapbox Light style.
          // To view all images available in a Mapbox style, open
          // the style in Mapbox Studio and click the "Images" tab.
          // To add a new image to the style at runtime see
          // https://docs.mapbox.com/mapbox-gl-js/example/add-image/
          // 'icon-image': 'star-15',
          // 'icon-size': 1.5,
            'icon-allow-overlap': true,
            'text-field': '{name}',
            'text-font': [
            'Open Sans Bold',
            'Arial Unicode MS Bold'
            ],
            'text-size': 11,
            'text-transform': 'uppercase',
            'text-letter-spacing': 0.05,
            'text-offset': [0, 1.5]
            },
            'paint': {
            'text-color': '#202',
            'text-halo-color': '#fff',
            'text-halo-width': 2
            },
            'filter': ['==', '$type', 'Point']
        });
      });
</script>
</br>

### day0 出发 追太阳的孩子
坐地铁到大兴机场。飞机在雾中起飞，窗外除了机翼什么也看不见。不久飞机冲破云层，蓝天重新出现。身侧有金色的夕照相伴，旅行的精神终于振作起来。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712214124.jpg" caption="gogogo" title=" " >}}


临落地西宁，天低地远，大地千沟万壑，起伏不定。在机场出口，一行四人会合。在停车场的时候，骤然下起豆大的雨来，这天气的脾气和南方颇为相似。

晚上去夜市补充能量，然后整理行装。

西行之旅堂堂开始！

### day1 我的心脏怦怦跳
起床，空气有点凉，大约10度。

早餐后开车从西宁市区出发，过了收费站，在巍峨群山之间穿行，因为气温尚不高，山间有云雾缭绕。对西北的初印象是山多，天穹更低，视野开阔，地平线在极远处。

到了此行的第一站，日月山。景区门口有人招徕游客与牦牛骆驼合影，之后会发现几乎青海的每个景点都有这项业务。日月山上有一个小博物馆——湟源古道博物馆，文成公主庙和文成公主像以及日亭与月亭，司机说文成公主曾至此吧啦吧啦，然而我对这一类传说奇谈是很不信的。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712215127.jpg" caption="小博物馆没什么好看的" title=" ">}}

沿着阶梯上山，这才感觉到呼吸比在平原更累，体会到含氧量之低。毕竟此山平均海拔4000m。日月亭在山顶，山上罡风很烈，待久了觉得冷。

**评价：日月山景区没什么底蕴，景色寻常，不值得花钱买票。**

离开日月山，途经倒淌河景区，只是一条凑巧向西流的普通河流罢了，谁要是花钱买票进去看可就**上大当**了。

继续行进到青海湖，湖确实很大，水天相接。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712215722.jpg" caption="青海湖" title=" ">}}

此时日近正午，阳光很强，眼中万物都似乎在一层白色滤镜之后。去青海旅游，**墨镜是必需品**。我们沿着湖岸漫步，打水漂玩，亦不能免俗，骑牦牛拍了游客照。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712215813.jpg" caption="打盹的牦牛" title=" ">}}

午饭司机带我们在景区附近吃的，贵而难吃，我颇不满意。

继续我们的旅途，青海湖的确很大，一直在视野之内。坐在车里看天，云层很厚，积压在远处的山上。时不时会下起一阵小雨，道路两旁能看见小股的羊群和牦牛群。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712220207.jpg" caption="黑云" title=" ">}}

我们还看到了溯游而上产卵的黄鱼。离开青海湖后在起伏的丘陵间前进。因为时间尚早，我们决定提前第二天的行程，去往茶卡盐湖。路上没有信号，真正进入了荒野。

到达茶卡盐湖是下午四点钟，天已转晴，阳光很暖，中和了凛凛的风，如果要上午去恐怕得多加几件衣服。从天空之镜景区入口到景点需要先坐景区大巴再坐观光小火车，当然都要买票的。青海的景点都喜欢这种一鱼多吃的分割售票方式，令我腹诽。

盐湖景色确实好，但一定要带着墨镜做好防晒，不然待不了多久眼睛便吃不消了。现场有出租鞋套供游客下湖游玩。盐湖最佳的景色应该是日出和日落。本想在茶卡盐湖看夕阳的，但是当地**八点半才日落**，实在饿得等不到那个时间。我们不到七点就往回走了。

**个人评价茶卡盐湖是值得去的景点。**

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712220344.jpg" caption="茶卡盐湖" title=" ">}}

从茶卡盐湖返程一直身体不适，脑壳痛。9点吃过晚饭——当地的炕锅，胃口不好没吃多少，10点便躺下睡了。睡着没两个小时，心跳得厉害，不由得醒了。深呼吸调整，心跳逐渐放缓。小伙伴给我送来了氧气瓶备用。起初我怀疑是高原反应，但是一系列证据表明真凶另有其人：
1. 茶卡海拔3000m左右，之后几天我在更高海拔活动也没感到不适。
2. 心悸醒来时的症状包括发热和多尿，这不是高反的症状。而我睡前因为小感冒的缘故吃了连花清瘟胶囊，恐怕肾脏高强度工作的原因是它。
3. 当天早上我吃了连花清瘟胶囊，上午坐车精神不振，下午茶卡开始感到头痛和呼吸不畅。

促使我下这个判断的主要依据是2，是药三分毒，我看连花清瘟能有七分。反省自己因为近两年没生病过而过于自信，药还是不能乱吃的。小病上猛药就是自己折腾自己，算是教训吧。

### day2 青海长云暗雪山
睡得很差，起床身体依然不适。注意深呼吸的节律尽量让自己舒服一些，~~练习呼吸法，加入鬼杀队~~。

开车离开茶卡镇，沿着G315前往翡翠湖，3h后进入德令哈市。突发奇想，公路旅行的实质就是猴子们利用铁甲壳虫的高速位移。路过尕海，只能看见细细的一线。一路上我基本在睡觉，感觉好多了。

之前下过雨，路旁积的雨水蒸干了，留下白色的盐。盐碱地上只能生长矮小的灌木。进入柴达木盆地后，地面确实平整了许多。

上午十点，到达第二日的第一站可鲁克湖，一个很偏很小的景点，甚是粗糙的开发，仅仅是围了块地，连脚踏船项目都没有。蚊虫之多令人震惊，其次是水鸟的数量，游人稀少，算上我们可能也就不到30人吧。可以说**去了就是上当**，尽管门票卖得不贵。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712222849.jpg" caption="可鲁克湖" title=" ">}}

<!--发现iOS的指南针可以显示当前海拔，临近大柴旦海拔3180m，小于之前的日月山，甚至稍高于昨天的茶卡。看来身体的不适不应该是高反的缘故，多半是休息不足+连花清瘟。后者有更大的嫌疑，成年人尚且如此，这药更不该给小孩用了。以后还是备一点好喝好用的金银花。-->

下午三点，到达大柴旦的翡翠湖，这个景点还算不错。巨大的云在天上浮动，向山岭投下连绵的阴影，远山的高处有点点积雪。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712220551.jpg" caption="翡翠湖" title=" ">}}

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712221705.jpg" caption="这个湖很大却不受游人喜爱，大概是颜色不够漂亮" title=" ">}}

翡翠湖是一群星星点点分布的小池塘，湖水多为翠绿色，当然纯正的程度有所区别，有的浑浊，有的清亮。细说起来它和前一天的茶卡盐湖属于同类。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/202110221240295.webp" caption="水波" title=" ">}}

我们乘小火车在第一站下车，决定在各个小湖间随意行走直到出口。在龟裂的土地和结晶盐上行走需要一双舒适的鞋子，鞋底最好厚一些，便于趟过浅水处。我们就上演了一出当代小马过河。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712221840.jpg" caption="" title=" ">}}

西北的天气变幻无常，即便是晴天，头顶的云也可能突然下起雨来。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712221859.jpg" caption="雨云" title=" ">}}

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712221932.jpg" caption="蓝色湖水" title=" ">}}

走走停停，离出口还有1000m时，头顶突然下起大雨，甚至夹杂着小冰雹，瞬间激发了我的高原血统，冲刺怎么说冲刺:running_man:。狼狈到了出口雨就停了，真是来得快去得也快。

宿大柴旦。那边街头的行道树也是槐树，给我熟悉之感。

这两天吃的很一般，三餐都是应付应付，**厨子该好好反思**。

### day3 旷野之息
晨起沿着G3011国道出发，去见识G315的U型公路。这段路修的不错，没之前的颠簸。

九点多的时候路过小柴旦湖，波光粼粼，芳草萋萋，算是意外之喜。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712222004.jpg" caption="小柴旦湖" title=" ">}}

过了小柴旦湖就上了G315。20分钟后看见一条干枯的河床，通体浅红色，司机说叫做大地之血，已经干涸了两年多。下车拍照，玩了会无人机。如果有水的话这地方可以多看几眼，没水就算了。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712222029.jpg" caption="大地之血" title=" ">}}

10点钟左右到达U型公路，许多人在路旁停车，坐在路中央拍照。一条公路延伸到天地交界之处本是绝景，人味太重就没那种孤寂感了。往来的车很多，还有重型货运卡车，停车拍照并不安全，有交警在驱散和罚款。天很热，配合司机拍了几张游客照就撤退。

U型公路见面不如闻名，不必抱太大期待。

继续前进，12点时在一处不知名的雅丹地貌停下来，登上去望远。岩石表面是细软而滑的沙土，再次展示出一双好鞋子的重要性。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712222049.jpg" caption="无名雅丹" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712223241.jpg" caption="左上拍到了一架无人机" title=" ">}}

坐标：北纬37°37′24″  东经93°49′35″

{{< mapbox lng=94.550 lat=37.616 zoom=4 marked=true light-style="mapbox://styles/mapbox/streets-zh-v1" dark-style="mapbox://styles/mapbox/dark-v10">}}

继续开车不到一个小时就到了水上雅丹景区，其实就是盐湖+雅丹地貌的组合，我们有些审美疲劳了。在停车场遇到一个穿着P大学士服的哥们（从校徽认出的），不禁腹诽毕业照跑到这么远的地方拍有何意义呢？水上雅丹的售票方式依旧是传统艺能一鱼多吃。我们在景区里玩得最开心的居然是用自带干粮里的瓜子仁喂湖中黑顶红嘴的肥鸟们（PS：后来司机说这是海鸥）。

有一只鸟特别坏，占了一片领地，自己吃饱了还不许别的鸟进来吃食，否则就扑腾翅膀驱赶。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712223322.jpg" caption="疑似海鸥的鸟" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712223551.jpg" caption="这里的水也是绿色的" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712223619.jpg" caption="禁止攀爬" title=" ">}}

沿着G215去往南八仙魔鬼城，名字很怪，其实就是一片雅丹地貌群。登上其中一个小山包，耳旁只有风声低诉。当风止的时刻，天地间万籁俱寂，少有的体验。不过魔鬼城的景色千篇一律，远眺一周就足够了。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712223751.jpg" caption="南八仙魔鬼城：来路" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712223811.jpg" caption="南八仙魔鬼城：去路" title=" ">}}

返回大柴旦宿，聚餐吃了羊排，差强人意。

### day4 世之奇伟瑰怪非常之观
终于完整地睡了一觉，高原血统稳定了。在青海这几天气色不太好，因为有些缺氧，外加空气极其干燥，嘴唇泛着紫色。这一天走G3011（甘肃境内G215）前往敦煌，大概340km。早上吃了碗西红柿鸡蛋面（18rmb），居然比前一天的牛肉面（10rmb）还贵，不过胜在量大味道也不错。

西北的地平线就像贴图一样，灰白色、黛色的山层层叠叠，总怀疑自己身处于楚门的世界。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712223848.jpg" caption="山" title=" ">}}

一入甘肃地界是新修的高速，乘车体验瞬间up。晴空正好，向着当金山前进。翻越当金山的路没有修隧道，公路沿着山势蜿蜒向上直到海拔3620m。在巍峨的群山间行进，这段山路**奇险瑰丽**，看得我兴致盎然。我将其评为绝对不能打瞌睡的路段之一。

出了山区就进入酒泉市辖区内，海拔下降到2600m。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712223953.jpg" caption="在路上" title=" ">}}

接近下午一点时，我们到达了石油小镇。平心而论，这个景区就是一个丑陋的建筑工地，不配作为景点。不过那时的天气实在太好，需要一个下车散步的地方，外加学生半价票，个人感觉勉勉强强算不亏吧。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224143.jpg" caption="石油小镇" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224210.jpg" caption="烂尾的工地" title=" ">}}

离开，到阿克塞吃午饭。路上碰见了野骆驼。还有好几股龙卷风，将尘土吸上高天。西北的云都好大一朵，褐色的山地上有一团团黑色的巨大阴影，那就是云的影子。

到阿克塞后气候骤然一变，与当金山不同，空气都是热的，自然景观更新为戈壁沙漠。

继续向敦煌进发，路上发现空中某处在发白光，高度和角度基本不随车的前进而变化。经过我们的推理，确认为聚光太阳能热发电的发电塔。后来果然看见了从下而上汇聚去的光线。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224303.jpg" caption="发电塔（图源维基）" title=" ">}}

一路行驶。海拔持续下降，到了敦煌就只有1000m出头，高原血统不必开启了。我们先去住处避一阵子暑，6点钟去户外露营的场地，今天就在那里过一夜。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224355.jpg" caption="户外场所" title=" ">}}

到了之后先体验了一把沙漠摩托车，然后等到7点左右领滑沙板去沙丘玩滑沙。爬上沙丘的过程着实累人，一脚踩上去下陷加下滑，每一步都很耗体力，有一瞬觉得自己变成了西西弗斯。不建议租鞋套，因为戴了鞋套也没啥用，该进沙子还是进沙子。滑了三趟我便下去了，实在不想再爬沙丘。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224434.jpg" caption="沙丘上" title=" ">}}

8点40左右开饭，为当地的土火锅，阴差阳错我们真就坐小孩那桌，正合我意。菜品是各种蔬菜丸子，基本见不到肉，味道很差。饮料是差一个月过期的可乐，啤酒是不知名的牌子，我只好接纯净水喝。

这个露营的精华在于其晚会，给我狠狠上了一波土味教育，即便身为有两年经验的鉴土师的我也大受冲击。

<p><center>{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000857.jpg" caption="" title=" ">}}</center></p>

声波攻击+光污染，农村娱乐的经典路数。开局一只猴，说是拍西游记时六老师的替身，那就叫他六耳老师吧。伴着《云宫迅音》，六耳老师到台下与观众热情互动，国人对猴的热爱令我印象深刻，一群成年人争相与戏服猴子合影，可见大圣的群众基础是极好的。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224714.jpg" caption="六耳老师" title=" ">}}

六耳老师在台下转了一圈，上台表演了翻跟头、耍棍子等，完成了暖场任务便下去了。主持人终于登场，居然就是把头套去了的六耳老师，小班子就得个个是复合型人才。六耳老师献歌一曲《夜夜夜漫长》，别的不谈唱歌水平是在我之上的。不知道是不是提前安排好的托儿，有个老哥上去给六耳老师塞钱，还有人往台上放啤酒。台上的酒越来越多，六耳老师乃是酒中豪杰，面上毫无难色，干脆取了个大碗，把放上台的酒都倒了进去。然后伴着吵闹的BGM和台下的起哄声将酒喝完了（期间还有人往碗里倒酒）。这碗酒花了不少时间，六耳老师一边喝一边兼顾维持场上气氛说着骚话。写的简略一是我不喜喝酒，二是不能接受观众们从他人伤害其身体中取乐的习俗，不想喝可以不喝。或许六耳老师喝酒如喝水（那这波表演他在大气层），但是显然观众并不这么认为，正是六耳老师在强行喝下过量的酒这一事实令他们感到兴奋。无聊冰冷的快乐。

接着六耳老师出场的是阿豹老师，据说其曾经登上~~土味鼻祖~~山东卫视。阿豹老师的绝活是口中含火，手中拿着道具风火轮，一会儿含灭风火轮上的火苗，一会儿用口中的火重新点燃。最后阿豹老师口含酒精喷火，无甚新意但现场看还算精彩，只是杂技写出来难免干巴巴的。

之后六耳老师重新上台，带着观众做游戏，直到最后两名胜者可以乘摩托车去沙漠深处看星空。压轴的活动是大家围着篝火成圈，蹦迪土嗨。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224733.jpg" caption="围着篝火起舞，没去是因为不喜欢和陌生人牵手" title=" ">}}

两个人竟然撑起了两个小时的晚会，六耳老师和阿豹老师的业务能力属实可以的。节目很接地气，正合我不土不快的口味。

准备领帐篷露营时出现了一个乌龙事件，我们一行中某人的钱包放在行李架上的书包里丢掉了。于是我们在中控室里看了半个小时监控，最后发现是落在车里了，虚惊一场。

然后我们坐在舞台边上，看星空吹风扯淡，能看到一条淡淡的银河，十足惬意。一点多钟钻进小帐篷休息，不得不说密闭空间内的jio臭有点顶。沙漠晚上风很大，必须拉紧入口不让沙子进来。和衣而睡，帐篷底下垫了床单与隔热垫，躺在坚实的沙面上还挺舒服的。

三点钟起来试图拍星空，因为多云而失败。

### day5 Only hate the road
五点多，组织者开始用大喇叭叫醒人们，推销其乘摩托车去远处沙丘看日出的收费项目。风很冷，灌进帐篷，身下沙子的热量也已散尽，既是吵醒也是冻醒，起床等日出。大概六点半太阳升出地平线，景致普通。

回到市区用完早餐，九点半到达莫高窟。要乘坐大巴前往景区，入口处是一个写着“石室宝藏”的牌楼。我们购买的是应急票，看了四个洞窟。看的时候觉得绘画挺有意思，转身出门就全部忘记，就当**花钱支持文物保护**了，个人感受（100rmb）不算亏。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224807.jpg" caption="院史陈列馆的院子" title=" ">}}

下午回到住处休息，黄昏时出发步行前往鸣沙山月牙泉。景区很小，作为一个人造景点，我认为它名过其实，真正的月牙湾早就消散在过去的风沙中，现在看到的只是霸占着其尸体的蛊虫。往者不可谏。~~（说人话：不配卖这么贵的门票）~~

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712224910.jpg" caption="仿古的塔" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712225018.jpg" caption="再次爬上沙丘，这里有木爬梯会容易一些" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712225120.jpg" caption="这个角度勉强能看" title=" ">}}

晚上和另一队聚餐，去沙洲夜市逛了逛。这两天的行程很无聊，想回家了。

### day6 千里
今日出发去张掖，里程有600多公里，literally一日千里。中途在瓜州服务区休息，能吃到店家免费的西瓜和哈密瓜，味道还挺甜。但是他家一直和我推销牦牛肉干，有些招架不住。

> “本来138一斤，早上第一波客人100一斤。”</br>
> “我看你是诚心想买，说个价钱吧。”

我只顾着在一旁啃西瓜，没注意到同行人都走出去了，于是成了店家重点关照的对象。我本来说20块钱交个朋友，又一想这么开玩笑大概会被轰出去:roll_eyes:，赶紧羞射一笑逃了出去。

G30从敦煌到嘉峪关，路上风光一般，都是些东部寻常景色或者普通戈壁，相较青海境内少了许多观看价值。但是甘肃省的公路养护得更好，更加平整。

中午吃一份盖饭，十二点半到嘉峪关景区门口，一个粗糙的人造景点门票竟然敢卖160rmb，是我们一路上所见最贵的，还大言不惭“天下第一雄关”，**普通却自信**，真不知道怎么评上5A的。在门口蹭了蹭，发现连拍游客照的价值都没有，转身就走。

暑气蒸腾，大段路上睡觉。我甚至担心司机会不会疲劳，实在是赶路太久了。

经过总计6h的车程，终于到了张掖七彩镇。我们住在西侧，价格便宜些。下午6点从西门进入七彩丹霞，先直奔另一侧出入口吃了个k记，再折返参观。虽然山体光秃秃一片稍丑，但总体配得上票价。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712225210.jpg" caption="" title=" " >}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712225254.jpg" caption="" title=" " >}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712225603.jpg" caption="" title=" " >}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712225818.jpg" caption="" title=" " >}}

落日后离开。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712225834.jpg" caption="" title=" ">}}

### day7 天青色
今天要前往祁连县，走227国道先驱车2h至**扁都口**，入口处海拔2820m。地处河西走廊，景色翠绿像是到了南方。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712225909.jpg" caption="扁都口" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712230033.jpg" caption="青山" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712230103.jpg" caption="亮晶晶的水洼" title=" ">}}

翻越祁连山脉的公路在海拔3000m以上，足足开了一个多小时。和缓的山间平原是极佳的牧场，有数量极多的牦牛和羊。这段公路景色极美，有绿水青山，和风煦日，我同样将其评为绝对不能打瞌睡的路段。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712230221.jpg" caption="牧牦牛" title="🐂" >}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712230404.jpg" caption="牧羊，橘色油漆是为了标记自家的羊" title="🐐">}}

阿柔大寺——当地一个部落自己修建的寺庙，没啥好看的，不过票价很便宜，买不了吃亏买不了上当，就当支持民族团结了。

离开阿柔大寺的路也极美，郁郁葱葱的树木极多。回到青海东部以后，景色漂亮多了，相比之下张掖真是不毛之地。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712230600.jpg" caption="一面长树一面长草" title=" ">}}

到了祁连县城，被两山夹住的一个条状小城，一条主干道贯通全县，挺整洁漂亮的小城，我很喜欢。中午吃了当地评分第一的一家土火锅，很赞，厨子终于争气一回。

住在卓尔山下的村子——拉洞台村。在此之前我没有听过卓尔山的名字，它却成为了我此行**最大的惊喜**。山不高，我们打算看完日落去市区吃晚饭，所以特意六点才出发。出门时天空下着蒙蒙细雨，从入口乘小巴车到山上的观景平台，然后步行沿栈道上山。山上风很大，兼之下雨的缘故，很有些冷。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231156.jpg" caption="雨中上山" title=" ">}}

接近七点钟，到了山顶的烽火台四望，天空仍是灰蒙蒙的，无趣的景象，我想这无名小山便是如此了。为时尚早，我们决定继续往另一侧走走，事实证明这是此行最为正确的决定。

到了山的西侧，天空开始放晴，远望祁连县城。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712230806.jpg" caption="远望祁连县城" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231023.jpg" caption="栈道下全是兔子窝" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231038.jpg" caption="阿咪东索山" title=" ">}}

照片左侧的是阿咪东索山，相传其与脚下的卓尔山是一对恋人。往回走看见山坡上有一群羊正在吃草。又走几步看见一只野兔，褐色的皮毛，尾巴上有一撮白毛。我想起以前看到一种说法，捉野兔要把它从山上往下赶，因为野兔后腿发力，速度比前腿更快，下山会翻跟头。我忍不住想实践一下，结果一靠近，野兔直接迅捷步伐跑得没影。回头时发现了另一只更肥的野兔，我恍然大悟，恐怕这栈道下面有兔子窝，也就解释了为什么附近的草地上有那么多一粒一粒的黑色的兔子粪便。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/202110221241231.webp" caption="野兔" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231123.jpg" caption="另一只野兔" title=" ">}}

经过这一通折腾，太阳已经全然从云后露出了，阳光普照下，卓尔山显示出惊人的美。绵延的山丘覆盖着一层诱人的绿，斜照的阳光勾勒出错落有致的阴影，湛蓝的天空上浮动着乳白色的流云。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231225.jpg" caption="" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231255.jpg" caption="旺盛生长的草" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231315.jpg" caption="路标" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231340.jpg" caption="玻璃门上的虚假太阳" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231404.jpg" caption="" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231423.jpg" caption="美到不真实的绿" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231447.jpg" caption="最喜欢的一张" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231519.jpg" caption="" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231545.jpg" caption="现成的取景框" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231608.jpg" caption="风景画" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231623.jpg" caption="金色余晖" title=" ">}}

等到日落，天空中有一道火红的晚霞。
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231651.jpg" caption="火烧云" title=" ">}}


晚上在当地评分第二的一家烤肉店吃烤羊腿，好吃量大不贵三点全占了，美滋滋的一天。

### day8 归去来兮
五点不到醒来，听到鸡鸣决定去村里转转。东方天空中挂着一道下弦月，耳畔传来啾啾鸟鸣，风侵罗衣轻寒。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231751.jpg" caption="卓尔山很矮" title=" ">}}

沿着乡间小路往山上行，在田地之间信步，云慢慢泛起粉色。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712235730.jpg" caption="东方" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712231841.jpg" caption="放牛的村民" title=" ">}}

云像天空中的鱼群，往太阳的另一侧迁徙。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210712235924.jpg" caption="鱼一样的云1" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000552.jpg" caption="鱼一样的云2" title=" ">}}

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000003.jpg" caption="麦田" title=" ">}}

朝霞首先照在阿咪东索山的山头，给它染上一层暖橙色。这道橙色渐渐下移，先是到了山腰，再继续向下。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000049.jpg" caption="" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000132.jpg" caption="" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000340.jpg" caption="" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000435.jpg" caption="露水" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000458.jpg" caption="霞光万道" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000513.jpg" caption="希望的田野" title=" ">}}

6点57分，太阳终于从东方的山头出现，温暖的朝霞照在身上暖暖的。
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000618.jpg" caption="" title=" ">}}
{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000736.jpg" caption="" title=" ">}}

心满意足地回到村中，吃过早点离开了这个小而美的县城。这一天没安排什么值得期待的景点，主要内容是走走停停回到西宁赶飞机。

再次确认了海拔，我在祁连3600m自由活动毫无问题，在茶卡的头疼绝对和连花清瘟脱不了干系，害得我难受两天，这药大有问题。

沿着来路离开祁连县，正好赶上牧人赶牦牛和羊群去草场，大批牛羊连绵几千米，很有意思。

上午十点在祁连的一处草原停下，地上有很多兔鼠打的洞。这些老鼠也懂得狡兔三窟的道理，一靠近就躲进洞里，不知道跑到哪个出口了。见到的兔鼠一只只都圆鼓鼓的，看来在草原上吃得很不错。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713001014.jpg" caption="兔鼠（图源网络）" title="🐇+🐭" >}}

十一点半远观了岗什卡雪峰，接着去门源的油菜花田下车走了走。和另一队会合吃了午饭。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713000833.jpg" caption="茂盛生长" title=" ">}}

五彩斑斓的羊群，显然是各家混养的，为了区分用油漆喷上不同的颜色。牦牛的话可能在耳朵上还会戴着不同的布带。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713001044.jpg" caption="混养的羊群" title=" ">}}

翻山越岭九曲十八弯离开门源。G227也是一段景致不错的山路，有水库，草山，树山。道路百转千回，两车道的宽度经常迎面开来重型卡车呼啸而过，惊险刺激。足足90min的车程，然而因为天气太热，我基本在车上睡过去了。

{{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713001105.jpg" caption="山路很高" title=" ">}}

到了宝库乡后才道路和缓起来。继续一路昏倦地去往机场。

不知道是不是我们一路的运气太好，遇上了好天气，最后临走时需要服从人品守恒定律，逆天的事情接连发生。

1. 到了机场附近的宾馆，晚餐我与另一人决定外卖解决，剩下的两人小队打算去一家鱼火锅。到店发现，店家说水管爆了做不了饭——彳亍，换一家。结果接下来这家的操作才是真正的**逆大天**。贴下原文吐槽：

    > 这家店真的一颗星都不想给。</br>
五点十分点完菜，五点四十总共只上了十串羊肉串，问店里说菜还没下锅！因为赶飞机给厨师说不要做了，直接上米饭，结果上了两碗味道发酸的米，吃了几口实在难以下咽，于是结账走人，结帐的时候厨师说菜做好了，没时间吃要求打包，最骚的事情来了，老板说没有打包盒要出去买，又等了十分钟才打包好带走，钱倒是一分都没少收。</br>
真不明白这样的店是怎么能开下去的，来这家店吃饭，怕不是脑子被门挤了。

    我们怀疑为了收这道菜的钱，水煮肉片没熟就被厨房急急忙忙端出来了，所以最后根本没敢吃。

    后续：在向青海的消协投诉后的几天，店老板打来电话道歉，说当日不在店中。

2. 同学A在滴滴上打车去机场，等了几分钟终于分配了司机，结果司机发来消息说机场路难走不去。此时已经过了免费取消的时间，于是A就和他耗着。同时我开始叫车，过了几分钟A的订单被司机取消，又过了几分钟我分配到了司机，居然和A的是同一个人，依然说不去机场。对话如下：
    {{< image src="https://fastly.jsdelivr.net/gh/Lucas-0/IMG/img/20210713001135.png" caption="" title=" ">}}

    最下面还有两句，
    > 司机:“你可以去市委或者消协投诉我，你也知道路有多难走。”</br>
    我说:“第一次来贵宝地，真不熟。”

    然后司机取消了订单，此时A叫到了出租车，此事结束。（当然我如他所愿投诉了一波，毫无服务业自觉的人。）
3. 我和A的飞机的前序航班比预定时间晚了80分钟起飞，所以晚点是可以预见的。登上飞机后又因为目的地天津的雷雨延误了80分钟起飞。另两人的飞机，一个延误了7小时，另一个干脆取消了。
4. 到了天津后本来说是酒店接机，打电话给老板，他说车子轮胎爆了让我们自己打车过去。估计只是午夜懒得动弹了，我也不计较这一点，反正天津打车是容易的。只是撒这么明显的谎言太敷衍了，~~重要的是心意~~至少要编一个说得过去的吧。

这几件事单独发生的话也不过是旅途中常见的抗压测试，怪就怪在集中于一天内发生，让人的心态不由得波动。

---

旅行结束，下面开始技术总结。

1. 青海境内旅行质量更高，日程可以压缩，青甘环线6天为宜。我们这趟8天的旅行难免掺入了低质量的景点，后期也感到疲乏。
2. 优秀的成本控制归功于事先安排好了一路的住宿（队友立大功）。<!--10天全程开销不到6k，准确的数字可能为5.8k-->
3. 脖枕墨镜帽子是旅行必备，防晒霜到底有没有用永远是个谜，离开时面如重枣的我陷入沉思。
4. 自驾要谨慎考虑，那些山路要是交给同学来开的话我会提心吊胆的。至于司机的人品，这个就看运气了，幸而我们遇上的司机人还不错。
5. 行李托运前记得把箱子里的氧气瓶扔掉:collision:。

<!--游记真难写，有草稿还是写了5天，文字工作和挑选处理图片都很费劲-->



