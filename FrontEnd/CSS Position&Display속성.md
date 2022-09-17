# CSS Position&Display 속성

## Display속성

- HTML 내 Element 를 어떻게 보여줄지 결정
- **display : none | block | inline | inline-block**

### none

- Element를 **렌더링하지 않도록 설정**
- **visibility 속성을 hidden으로 설정한 것과 달리, 영역을 차지하지 않음**

**html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style> 
	div{
	    text-align: center;
	    background-color: cadetblue;
	}
	
	/* diplay속성의 none : 자리를 차지 안 함 */
	.display-none{ display: none }
	
	/* visibility속성의 hidden : 자리를 자치 */
	.invisible{ visibility: hidden }
    </style>
</head>
<body>

    <div class="display-none">1</div>
    <div>2</div>

    <div class="invisible">3</div>
    <div>4</div>

</body>
</html>
```

![https://user-images.githubusercontent.com/44748142/190874000-80ae8bdb-386c-451f-9dd2-fb0d4bce62ec.png](https://user-images.githubusercontent.com/44748142/190874000-80ae8bdb-386c-451f-9dd2-fb0d4bce62ec.png)

### block

- **줄 바꿈** 설정. 즉, 해당 요소의 다음 요소는 다음 줄에 위치
- ex) d**iv, p, h, li 등**
- **width, height, margin, padding 속성 사용 가능**
- span은 원래 줄바꿈 속성이 없지만 display속성을 block으로 설정하면서 줄바꿈과 width 설정이 가능해진 것을 볼 수 있음.

**html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
	span{
            margin: 10px;
	    text-align: center;
            background-color: cadetblue;
            display : block;
	}
        
	.span1{ width: 300px;}
      
    	.span2{ width: 200px;}
    </style>
</head>
<body>
    <span class="span1">span</span>
    <span class="span2">span</span>
</body>
</html>
```

![https://user-images.githubusercontent.com/44748142/190874391-03367016-3dd0-4a4b-aef1-900448bdc543.png](https://user-images.githubusercontent.com/44748142/190874391-03367016-3dd0-4a4b-aef1-900448bdc543.png)

### inline

- **줄 바꿈 없이 연속**으로 이어짐
- ex) **span, b, a 태그 등**
- **width, height 지정 불가능**
- **margin과 padding 속성은 좌우만 반영**되고, **상하 간격은 반영되지 않음**
- div는 block속성을 가지지만, display속성을 inline으로 설정하면서 줄 바꿈없이 연속으로 이어지면서 width 설정이 불가능해짐.

**html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
       
	div{
            margin: 10px;
            text-align: center;
            background-color: cadetblue;
            display : inline;
	}
        
        /* width 속성 적용 불가 */
	.div1{ width: 300px;}
        .div2{ width: 200px;}
    </style>
</head>
<body>
    <div class="div1">div</div>
    <div class="div2">div</div>
</body>
</html>
```

![https://user-images.githubusercontent.com/44748142/190874652-15ccd80a-078d-473e-b4c2-0126fc3d8a7f.png](https://user-images.githubusercontent.com/44748142/190874652-15ccd80a-078d-473e-b4c2-0126fc3d8a7f.png)

### inline-block

- block과 inline의 중간 형태
- **줄 바꿈이 없고, 크기 지정 및 margin과 padding 속성의 상하 간격 지정 가능**
- span은 크기 지정이 불가능하지만, display속성을 inline-block으로 설정하면서 width지정 가능해짐

**html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style> 
	span{
            margin: 10px;
            text-align: center;
            background-color: cadetblue;
            display : inline-block;
	}
        
	.span1{ width: 300px;}
        .span2{ width: 200px;}
    </style>
</head>
<body>
    <span class="span1">span</span>
    <span class="span2">span</span>
</body>
</html>
```

![https://user-images.githubusercontent.com/44748142/190874905-57ad4c2d-ea44-462a-b094-14edd1b07707.png](https://user-images.githubusercontent.com/44748142/190874905-57ad4c2d-ea44-462a-b094-14edd1b07707.png)

## Postition

- HTML 내 Element 위치를 지정
- **position: static | relative | absolute | fixed | sticky**

### static

- 기본값으로 element를 **문서 흐름에 맞춰 배치**
- **top, right, bottom, left와 같은 속성 사용불가** (float 속성은 가능!)

### relative

- **해당 요소가 static이었을 때 배치되는 위치를 기준으로 상대적 위치 지정**
- **top, right, bottom, left와 같은 속성 사용하여 배치**

### absolute

- 자신의 **상위 box속에서 절대적인 위치 지정**
- 상위 box의 기준은 **가장** **가까운 부모 요소 혹은 조상 요소 중 position 속성이 relative인 요소를 의미**
- **상위 요소 중 relative인 요소가 없다면 전체 문서가 기준**

### fixed

- **브라우저 창을 기준으로 고정된 위치** 지정
- **스크롤이 일어나도 고정된 좌표에 위치**

html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box-container{
	    margin: 40px;          
            height: 1000px;
	    border: 2px solid black; 
	}
	.box-container div{
            width: 200px;
	    text-align: center;
            background-color: cadetblue;
	}
    	/* static이므로 top, left속성 적용 불가능 */
	#box1 { position: static; top: 20px; left: 50px; }

   	/* relative이므로 흐름에 맞춰 위치해야하는 곳에서 top, left 속성값에 맞춰 배치*/
	#box2 { position: relative; top: 20px; left: 50px; }

    	/* absolute이므로 부모 요소 중 relative 속성값을 가진 요소를 기준으로 배치. 이 경우 relative 속성값을 가진 부모 없으므로 전체 문서 기준 */
	#box3 { position: absolute; top: 20px; right: 50px; }

    	/* fixed이므로 브러우저 창을 기준으로 고정 배치. 스크롤 작동시에도 고정 */
	#box4 { position: fixed; bottom: 20px; right: 50px; }

    	/* relative이므로 흐름에 맞춰 위치해야하는 곳에서 top, left 속성값에 맞춰 배치*/
    	#box5 { position: relative; top: 50px; left: 50px;}

    	/* absolute이므로 부모 요소 중 relative 속성값을 가진 요소를 기준으로 배치. 이 경우 부모 요소의 box5가 relative 속성값을 가지므로 해당 요소 기준으로 배치 */
    	#box6 { position: absolute; top: 50px; left: 50px;}
    </style>
</head>
<body>
    <div class="box-container">
		<div id="box1">static box</div>
		<div id="box2">relative box</div>
		<div id="box3">absolute box</div>
		<div id="box4">fixed box</div>
        <div id="box5"> relative box2
            <div id="box6">relative box2안의 absolute box</div>
        </div>
	</div>
</body>
</html>
```

![https://user-images.githubusercontent.com/44748142/190874025-a3ecc66f-bb04-4236-86bc-7bb3fa0db2b5.png](https://user-images.githubusercontent.com/44748142/190874025-a3ecc66f-bb04-4236-86bc-7bb3fa0db2b5.png)
