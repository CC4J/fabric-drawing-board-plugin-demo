<template>
  <div class="home">
		<div style="text-align:left;">
			<button @click="tapBrush(2)">brush1</button>
			<button @click="tapBrush(4)">brush2</button>
			<button @click="tapBrush(6)">brush3</button>
			<button @click="tapBrush(8)">brush4</button>
			<span style="margin-right: 50px"></span>
			<button @click="tapLine(2)">line1</button>
			<button @click="tapLine(4)">line2</button>
			<button @click="tapLine(6)">line3</button>
			<button @click="tapLine(8)">line4</button>
		</div>
		<div style="text-align:left;">
			<button @click="tapRect(2)">rect1</button>
			<button @click="tapRect(4)">rect2</button>
			<button @click="tapRect(6)">rect3</button>
			<button @click="tapRect(8)">rect4</button>
			<span style="margin-right: 50px"></span>
			<button @click="tapCircle(2)">circle1</button>
			<button @click="tapCircle(4)">circle2</button>
			<button @click="tapCircle(6)">circle3</button>
			<button @click="tapCircle(8)">circle4</button>
		</div>
		<div style="text-align:left;">
			<button @click="tapText(18)">text1</button>
			<button @click="tapText(24)">text2</button>
			<button @click="tapText(32)">text3</button>
			<button @click="tapText(48)">text4</button>
			<span style="margin-right: 50px"></span>
			<button @click="tapEraser(4)">eraser1</button>
			<button @click="tapEraser(12)">eraser2</button>
			<button @click="tapEraser(20)">eraser3</button>
			<button @click="tapEraser(28)">eraser4</button>
		</div>
		<div style="text-align:left;">
			画笔颜色： 
			<button @click="setBrushColor('#f00')">红</button>
			<button @click="setBrushColor('#0f0')">绿</button>
			<button @click="setBrushColor('#00f')">蓝</button>
		</div>
		<div style="text-align:left;">
			线条颜色： 
			<button @click="setStrokeColor('#f00')">红</button>
			<button @click="setStrokeColor('#0f0')">绿</button>
			<button @click="setStrokeColor('#00f')">蓝</button>
		</div>
		<div style="text-align:left;">
			填充色颜色： 
			<button @click="setFillColor('#f00')">红</button>
			<button @click="setFillColor('#0f0')">绿</button>
			<button @click="setFillColor('#00f')">蓝</button>
		</div>
		<div style="text-align:left;">
			背景色颜色： 
			<button @click="setBgColor('rgba(0,0,0,0)')">透明</button>
			<button @click="setBgColor('rgba(0,0,0)')">黑</button>
			<button @click="setBgColor('rgba(255,255,0)')">黄</button>
		</div>
		<div style="text-align:left;">
			<button @click="tapMove">move</button>
			<button @click="tapZoomDown">zoom -</button>
			<button @click="tapZoomUp">zoom +</button>
			<button @click="tapUndo">undo</button>
			<button @click="tapRedo">redo</button>
			<button @click="tapClear">clear</button>
			<button @click="tapSave">save</button>
		</div>
		<div style="height:600px;border:1px solid #000;over-flow:hidden;">
			<canvas id="myCanvas"></canvas>
		</div>
  </div>
</template>

<script>
import FabricDrawingBoard from 'fabric-drawing-board'
export default {
  name: "Home",
	data() {
		return {
			fdb: null
		}
	},
	mounted() {
		this.fdb = new FabricDrawingBoard({canvasId: 'myCanvas'})
		console.log(this.fdb)
	},
	methods: {
		setBrushColor(color) {
			this.fdb.setBrushColor(color)
		},
		setStrokeColor(color) {
			this.fdb.setStrokeColor(color)
		},
		setFillColor(color) {
			this.fdb.setFillColor(color)
		},
		setBgColor(color) {
			this.fdb.setBgColor(color)
		},
		tapBrush(size) {
			this.fdb.setBrushSize(size)
			this.fdb.drawBrush()
			console.log(this.fdb)
		},
		tapLine(size) {
			this.fdb.setStrokeSize(size)
			this.fdb.drawLine()
		},
		tapRect(size) {
			this.fdb.setStrokeSize(size)
			this.fdb.drawRect()
		},
		tapCircle(size) {
			this.fdb.setStrokeSize(size)
			this.fdb.drawCircle()
		},
		tapText(size) {
			this.fdb.setFontSize(size)
			this.fdb.drawText()
		},
		tapEraser(size) {
			this.fdb.setEraserSize(size)
			this.fdb.useEraser()
		},
		tapMove() {
			this.fdb.useMove()
		},
		tapZoomDown() {
			this.fdb.canvasZoomDown()
		},
		tapZoomUp() {
			this.fdb.canvasZoomUp()
		},
		tapUndo() {
			this.fdb.canvasUndo()
		},
		tapRedo() {
			this.fdb.canvasRedo()
		},
		tapClear() {
			this.fdb.canvasClear()
		},
		tapSave() {
			this.fdb.canvasExport(dataURL => {
				const link = document.createElement('a');
        link.download = 'canvas.png';
        link.href = dataURL;
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
			})
		}
	}
};
</script>

<style>
button{
	min-width: 100px;
	margin-right: 10px;
	margin-bottom: 5px;
}
</style>
