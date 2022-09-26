# Js-DON-1-drawing-app
אפליקציית צייר
	JS
	
	// בחירת אלמנטים
	const canvas = document.getElementById('canvas'); 
	const increaseBtn = document.getElementById('increase');
	const decreaseBtn = document.getElementById('decrease');
	const sizeEL = document.getElementById('size');
	const colorEl = document.getElementById('color');
	const clearEl = document.getElementById('clear');
	const ctx = canvas.getContext('2d'); // בשביל להגדיר שאפשר לצייר בתוך המשטח
	let size = 10 //משתנה לגודל ראשוני
	let isPressed = false
	colorEl.value = 'black' // משתנה לצבע ראשוני
	let color = colorEl.value
	let x
	let y
	//  חישוב מיקום העכבר בצירים כאשר לוחצים עליו
	canvas.addEventListener('mousedown', (e) => {
	    isPressed = true
	    x = e.offsetX
	    y = e.offsetY
	})
	// ביטול החישוב כאשר לא לוחצים על העכבר
	canvas.addEventListener('mouseup', (e) => {
	    isPressed = false
	    x = undefined
	    y = undefined
	})
	canvas.addEventListener('mousemove', (e) => {
	    if(isPressed) {
	        const x2 = e.offsetX
	        const y2 = e.offsetY
	        drawCircle(x2, y2)
	        drawLine(x, y, x2, y2)
	        x = x2
	        y = y2
	    }
	})
	// פונקציה שתאפשר לצייר עיגול
	function drawCircle(x, y) {
	    ctx.beginPath();
	    ctx.arc(x, y, size, 0, Math.PI * 2)
	    ctx.fillStyle = color
	    ctx.fill()
	}
//  פונקציה שתאפשר לצייר צייר עם העיגול שורה
	function drawLine(x1, y1, x2, y2) {
	    ctx.beginPath()
	    ctx.moveTo(x1, y1)
	    ctx.lineTo(x2, y2)
	    ctx.strokeStyle = color
	    ctx.lineWidth = size * 2 // להכפיל בשביל חישוב שיהיה קו רצוף
	    ctx.stroke()
	}
	//  פונקציה לשינוי גדול העיגול
	function updateSizeOnScreen() {
	    sizeEL.innerText = size
	}
	// תנאים להגבלת גודל
	increaseBtn.addEventListener('click', () => {
	    size += 5
	    if(size > 50) {
	        size = 50
	    }
	    updateSizeOnScreen()
	})
	decreaseBtn.addEventListener('click', () => {
	    size -= 5
	    if(size < 5) {
	        size = 5
	    }
	    updateSizeOnScreen()
	})
	// הפעלת כפתורים
	colorEl.addEventListener('change', (e) => color = e.target.value)
	// כפתור לניקוי המשטח ציור
	clearEl.addEventListener('click', () => ctx.clearRect(0,0, canvas.width, canvas.height))
![image](https://user-images.githubusercontent.com/56929518/192363635-29843793-db36-47e4-9617-ec20ef51a83c.png)
