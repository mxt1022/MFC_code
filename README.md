# MFC_code

# MFC

### `Bresenham`中点划线

###### 参数版：

```c++
int x, y, a, b,d, d1, d2, d;
	int x1 = 10, x2=221, y1=10, y2=90;
	a=y1-y2,b=x2-x1;
	d = 2 * a + b; d1 = 2 * a; d2 = 2 * (a + b);
	x = x1; y = y1;
	pDC->SetPixel(x, y, RGB(0, 23, 23));
	while (x<x2){
		x += 1;
		if (d<0){
			y++;
			d += d2;
		}
		else{
			d += d1;
		}
		pDC->SetPixel(x, y, RGB(0, 23, 23));
	}
```

###### 函数版：

```c++
void midpointline(int x1,int y1,int x2,int y2,int color){
	int x, y, a, b,d, d1, d2, d;a=y1-y2,b=x2-x1;
	d = 2 * a + b; d1 = 2 * a; d2 = 2 * (a + b);
	x = x1; y = y1;
	pDC->SetPixel(x, y, RGB(0, 23, 23));
	while (x<x2){
		x += 1;
		if (d<0){
			y++;
			d += d2;
		}
		else{
			d += d1;
		}
		pDC->SetPixel(x, y, RGB(0, 23, 23));
	}
}
```

### `DDA`算法

###### 参数版：

```c++
int x1 = 0, y1 = 0, x2 = 255, y2 = 255, x;
	float k, dx, dy, y = y1;
	dx = x2 - x1, dy = y2 - y1; k = dy / dx;
	for (x = x1; x <= x2; x++){
		pDC->SetPixel(x, (int)(y + 0.5), RGB(0, 0, 255));
		y += k;
	}
```

```c++
int x,x1=10,x2=255,y1=10,y2=90;
	float k, dx, dy, y = y1;
	dx = x2 - x1, dy = y2 - y1, k = dy / dx;
	for (x = x1; x <= x2; x++){
		pDC->SetPixel(x, (int)(y + 0.5), RGB(0, 0, 0));
	}
```

###### 函数版：

```c++
void dda(int x1,int x2,int y1,int y2,int color){
	float k,dx,dy,y=y1;
    dx=x2-x1,dy=y2-y1;k=dy/dx;
    for(x=x1;x<=x2;x++){
		pDC->SetPixel(x,(int)(y+0.5),RGB(0,0,0));
        y+=k;
    }
}
```

### `WU反走样算法`

###### 参数版：

```c++
int x, y, a, b, d1, d2, d;
	int x1 = 0, x2 = 255, y1 = 0, y2 = 255;
	float k, e;
	int color = RGB(23, 23, 23);
	k = 1.0*(y2 - y1) / (x2 - x1);
	e = 0.0;
	x = x1, y = y1;
	pDC->SetPixel(x, y,color);
	while (x < x2){
		x++;
		e += k;
		if (e >= 1){
			y += 1;
			e -= 1;
		}
		pDC->SetPixel(x, y, e*color);
		pDC->SetPixel(x, y, (1 - e)*color);
	}
```

###### 函数版：

```c++
void ddd_wu(int x1,int y1,int x2,int y2,int color,CDC*pDC){
	int x,y,a,b,d1,d2,d;
    float k,e;
    k=1.0*(y2-y1)/(x2-x1);
    e=0.0;
    x=x1,y=y1;
    pDC->SetPixel(x,y)
    while(x<x2){
		x++;
        e+=k;
        if(e>=1){
            y+=1;
            e-=1;
        }
        pDC->SetPixel(x,y,e*color);
        pDC->SetPixel(x,y,(1-e)*color);
    }
}
```

### `1/4圆画法`

###### 函数版：

```c++
void midpointcircle(int xc,int yc,int r,int color){
    int x=0,y=r,d=1-r;
    WholeCircle(xc,yc,x,y,color);
    while(x<=y){
        if(d<0){
            d+=2*x+3;
            x++;
        }
        else{
            d+=2*(x-y)+5;
            x++;
            y--;
        }
        WholeCircle(xc,yc,x,y,color)
    }
}
void WholeCircle(int xc,int yc,int x,int y,int color){
	pDC->SetPixel(xc+x,yc+y,color);
    pDC->SetPixel(xc-x,yc+y,color);
    pDC->SetPixel(xc+x,yc-y,color);
    pDC->SetPixel(xc-x,yc-y,color);
    pDC->SetPixel(xc+y,yc+x,color);
    pDC->SetPixel(xc-y,yc+x,color);
    pDC->SetPixel(xc+y,yc-x,color);
    pDC->SetPixel(xc-y,yc-x,color);
}
```

### `Bresenham画圆算法`

```c++
void BresenhamCircle(int xc,int yc,int r,int color，CDC*pDC){
	int x=0,y=r,d=3-2*r;
    while(x<y){
		WholeCircle(xc,yc,x,y,color,pDC);
    	if(d<0)d=d+4*x+6;
        else{d=d+4*(x-y)+10;y--;}
         x++;
    }
    if(x==y)WholeCircle(xc,yc,x,y,color,pDC)
}
void WholeCircle(int xc,int yc,int x,int y,int color,CDC*pDC){
	pDC->SetPixel(xc+x,yc+y,color);
    pDC->SetPixel(xc-x,yc+y,color);
    pDC->SetPixel(xc+x,yc-y,color);
    pDC->SetPixel(xc-x,yc-y,color);
    pDC->SetPixel(xc+y,yc+x,color);
    pDC->SetPixel(xc-y,yc+x,color);
    pDC->SetPixel(xc+y,yc-x,color);
    pDC->SetPixel(xc-y,yc-x,color);
}

```

### `椭圆生成算法`：

```c++
void MidpointEllipse(int xc, int yc, int a, int b, int color, CDC*pDC){
	int aa = a*a, bb = b*b;
	int twoaa = 2 * aa, twobb = 2 * bb;
	int x = 0, y = b;
	int dx = 0, dy = twoaa*y;
	int d = (int)(bb + aa*(-b + 0.25) + 0.5);
	WholeEllipse(xc, yc, x, y, color, pDC);
	while (dx<dy){
		x++; dx += twobb;
		if (d<0)d += bb + dx;
		else{
			y--;
			dy -= twoaa;
			d += bb + dx - dy;
		}
		WholeEllipse(xc, yc, x, y, color, pDC);
	}
	d = (int)(bb*(x + 0.5)*(x + 0.5) + aa*(y - 1)*(y - 1) - aa*bb + 0.5);
	while (y>0){//下半段生成
		y--;
		dy -= twoaa;
		if (d>0)d += aa - dy;
		else{
			x++; dx += twobb;
			d += aa - dy + dx;
		}
		WholeEllipse(xc, yc, x, y, color, pDC);
	}
}
void WholeEllipse(int xc, int yc, int x, int y, int color, CDC*pDC){
	pDC->SetPixel(xc + x, yc + y, color);
	pDC->SetPixel(xc - x, yc + y, color);
	pDC->SetPixel(xc + x, yc - y, color);
	pDC->SetPixel(xc - x, yc - y, color);
}
```

###### 算法改进：

