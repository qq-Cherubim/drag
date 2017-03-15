# drag
capture and drag
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}
			#box{
				position:absolute;
				width: 100px;
				height: 100px;
				background: brown;
			}
			#others{
				position: absolute;
				left: 500px;
				top: 300px;
				width: 200px;
				height: 200px;
				background: deeppink;
			}
		</style>
	</head>
	<body>
	你好
		<div id="box">
			
		</div>
		<div id="others">
			
		</div>
	</body>
	<script type="text/javascript">
		var box = document.getElementById('box');
		
		//鼠标初始位置
		var startP = {left:0,top:0};
		//元素初始位置
		var elementP = {left:0,top:0};
		box.onmousedown = function(ev){
			var ev = ev || event;
			
			//获取鼠标位置
			startP.left = ev.clientX;
			startP.top = ev.clientY;
			
			//获取元素位置
			elementP.left = box.offsetLeft;
			elementP.top = box.offsetTop;
			
			//全局捕获  处理ie8
			if(box.setCapture){
				box.setCapture();
			}
			
			
			document.onmousemove = function(ev){
				var ev = ev || event;
				
				//鼠标现在的位置
				var nowP = {};
				nowP.left = ev.clientX;
				nowP.top = ev.clientY;
				
				//鼠标的距离差
				var disX = 0;
				var disY = 0;
				disX = nowP.left - startP.left;
				disY = nowP.top - startP.top;
				
				box.style.left = elementP.left + disX + 'px';
				box.style.top = elementP.top + disY + 'px';
				
			}
			
			document.onmouseup = function(){
				document.onmousemove = document.onmouseup = null;
				if(box.releaseCapture){
					box.releaseCapture()
				}
				
			}
		
			//dom0
			return false;
		}
		
		
		
		
	</script>
</html>
