
//全是代码

package tuxiang;

import java.applet.*;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.*;
import javax.imageio.*;

public class huatu extends Applet{
	int ku=0,ku1=0,area7[];
	 String kus [],namelj;
	 double jx;
/*int i=1;
Color c=new Color(0,0,100);
 public void init(){
 setBackground(c);
 }
 public void paint(Graphics g){
 i = i+8; 
 if(i>160)
	 i=1;
 g.setColor(Color.red);
 g.fillRect(i,10,20,20);
 g.drawString("我正学习update()方法",100,100);
 try{
  Thread.sleep(100);
 }
 catch(InterruptedException e){}
 repaint();
 }
 public void update(Graphics g){
 g.clearRect(i,10,200,100);//不清除"我正在学习update()方法"
 paint(g);
 }*/
 Color c=new Color(0,0,100);
 public void init(){
 setBackground(c);
 }
 public void paint(Graphics g){
	 String lj="",name = null;
	 ku=0;
	 ku1=0;
	 lj=getImagePixel("F:\\计算机图形学\\ku-sb\\tld1.jpg");
	 System.out.println(lj);
	 File file = new File("F:\\计算机图形学\\ku-sb\\tld1.jpg");
	 BufferedImage bi = null;
      try {
         bi = ImageIO.read(file);
     } catch (IOException e) {
     
         e.printStackTrace();
     } 
     g.drawImage(bi,0,0,300,400, null);
	 File file1 = new File(lj);
	 BufferedImage bi1 = null;
      try {
         bi1 = ImageIO.read(file1);
     } catch (IOException e) {
     
         e.printStackTrace();
     } 
     g.drawImage(bi1,300,0,300,400, null);
     //防止文件建立或读取失败，用catch捕捉错误并打印，也可以throw;
     //不关闭文件会导致资源的泄露，读写文件都同理
     try (//FileReader reader = new FileReader(namelj);
    		 BufferedReader br=new BufferedReader(new InputStreamReader(new FileInputStream(namelj), "UTF-8")); // 建立一个对象，它把文件内容转成计算机能读懂的语言
     ) { 
                  name = br.readLine();
                  System.out.println(name);
        } catch (IOException e) {
         e.printStackTrace();
     }
     if (jx>1330000)
    	 name="不认识此人 ，"+"但与"+name+"最相似！";
     else
     {}
     g.setColor(Color.red);
     g.setFont(new Font("宋体", Font.BOLD, 50));
     g.drawString(name,0,500);
     
     
	 }
 public String getImagePixel(String image) {
	 String pathname = "F:\\计算机图形学\\ku1\\ku.txt"; 
	 String line="10";
     //防止文件建立或读取失败，用catch捕捉错误并打印，也可以throw;
     //不关闭文件会导致资源的泄露，读写文件都同理
     try (FileReader reader = new FileReader(pathname);
          BufferedReader br = new BufferedReader(reader) // 建立一个对象，它把文件内容转成计算机能读懂的语言
     ) { 
                  line = br.readLine();
                  System.out.println(line);
        } catch (IOException e) {
         e.printStackTrace();
     }
   ku=Integer.parseInt(line);
   kus=new String [ku];
	 File file1=new File("F:\\计算机图形学\\ku");
       getDirectory(file1);
       
		int i;
		
       int[] rgb = new int[3];
       File file = new File(image);
      BufferedImage bi = null;
       try {
          bi = ImageIO.read(file);
      } catch (IOException e) {
      
          e.printStackTrace();
      }
      int width = bi.getWidth();
      int height = bi.getHeight();
      int minX = bi.getMinX();
      int minY = bi.getMinY();
      for(int x = minX; x < width; x++) {
     	 for(int y = minY; y < height; y++){
              //获取包含这个像素的颜色信息的值, int型
              int pixel = bi.getRGB(x, y);
              //从pixel中获取rgb的值
              rgb[0] = (pixel & 0xff0000) >> 16; //r
              rgb[1] = (pixel & 0xff00) >> 8; //g
             rgb[2] = (pixel & 0xff); //b
     	 }
      }
             //System.out.println("x:"+x+"y:"+y);
             //System.out.println("r:"+rgb[0]+"g:"+rgb[1]+"b:"+rgb[2]);
      int a=(width-minX),b=(height-minY);
      int area1[] = new int [400];
      int area2[] = new int [400];
      int area3[] = new int [400];
      int area4[] = new int [400];
      int area5[] = new int [400];
      int area6[] = new int [2000];
      area7= new int [2000];
      int pixel;
      i=0;
      int r=0;
      for(int x = (a/4)-10; x < (a/4)+10; x++) {
     	 for(int y = (b/4)-10; y < (b/4)+10; y++){
     		 pixel = bi.getRGB(x, y);
              //从pixel中获取rgb的值
              rgb[0] = (pixel & 0xff0000) >> 16; //r
              rgb[1] = (pixel & 0xff00) >> 8; //g
             rgb[2] = (pixel & 0xff); //b
     	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
     	area1[i]=fft2(x, y, r, 20, 20);
     	i++;
     	 }
     }
      i=0;
      for(int x = (a/4)-10; x < (a/4)+10; x++) {
     	 for(int y = (b*3/4)-10; y < (b*3/4)+10; y++){
     		 pixel = bi.getRGB(x, y);
              //从pixel中获取rgb的值
              rgb[0] = (pixel & 0xff0000) >> 16; //r
              rgb[1] = (pixel & 0xff00) >> 8; //g
             rgb[2] = (pixel & 0xff); //b
     	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
     	area2[i]=fft2(x, y, r, 20, 20);
     	i++;
     	 }
     }
      i=0;
      for(int x = (a*3/4)-10; x < (a*3/4)+10; x++) {
     	 for(int y = (b/4)-10; y < (b/4)+10; y++){
     		 pixel = bi.getRGB(x, y);
              //从pixel中获取rgb的值
              rgb[0] = (pixel & 0xff0000) >> 16; //r
              rgb[1] = (pixel & 0xff00) >> 8; //g
             rgb[2] = (pixel & 0xff); //b
     	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
     	area3[i]=fft2(x, y, r, 20, 20);
     	i++;
     	 }
     }
      i=0;
      for(int x = (a*3/4)-10; x < (a*3/4)+10; x++) {
     	 for(int y = (b*3/4)-10; y < (b*3/4)+10; y++){
     		 pixel = bi.getRGB(x, y);
              //从pixel中获取rgb的值
              rgb[0] = (pixel & 0xff0000) >> 16; //r
              rgb[1] = (pixel & 0xff00) >> 8; //g
             rgb[2] = (pixel & 0xff); //b
     	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
     	area4[i]=fft2(x, y, r, 20, 20);
     	i++;
     	 }
     }
      i=0;
      for(int x = (a/2)-10; x < (a/2)+10; x++) {
     	 for(int y = (b/2)-10; y < (b/2)+10; y++){
     		  pixel = bi.getRGB(x, y);
              //从pixel中获取rgb的值
              rgb[0] = (pixel & 0xff0000) >> 16; //r
              rgb[1] = (pixel & 0xff00) >> 8; //g
             rgb[2] = (pixel & 0xff); //b
     	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
     	area5[i]=fft2(x, y, r, 20, 20);
     	i++;
     	 }
     }
      for (i=0;i<400;i++)
      {
      	area6[i]=area1[i];	
      	System.out.println("pic0"+":"+area6[i]);
      	
      }
      for (i=400;i<800;i++)
      {
      	area6[i]=area2[i-400];	
      	System.out.println("pic0"+":"+area6[i]);
      	
      }
      for (i=800;i<1200;i++)
      {
      	area6[i]=area3[i-800];	
      	System.out.println("pic0"+":"+area6[i]);
      	
      }
      for (i=1200;i<1600;i++)
      {
      	area6[i]=area4[i-1200];	
      	System.out.println("pic0"+":"+area6[i]);
      	
      }
      for (i=1600;i<2000;i++)
      {
      	area6[i]=area5[i-1600];	
      	System.out.println("pic0"+":"+area6[i]);
      	
      }
      for (i=0;i<2000;i++)
      area7[i]=area6[i];
		double xs []= new double [ku];
        for (i=0;i<ku;i++)
	            {
        	      xs[i]=bl(kus[i],i+1);
	            }
        int k=0;
        double k1=xs[0];
         for (i=0;i<ku;i++)
         {
	       if (k1>xs[i])
	       {
	    	   k1=xs[i];
	    	   k=i;
	       }
         }
         jx=k1;
         String s="",s1="";
         s="F:"+"\\\\"+"计算机图形学"+"\\\\"+"ku"+"\\\\"+"p"+k+".jpg";
         s1="F:"+"\\\\"+"计算机图形学"+"\\\\"+"ku-t"+"\\\\"+"p"+k+".txt";
         namelj=s1;
         for (i=0;i<ku;i++)
         { System.out.println("ejldjl  "+i+":     "+xs[i]);}
        return s;
        
	            
	        /* try {
	             OutputStream ops = new FileOutputStream(new File("F:\\计算机图形学\\huaduo1.jpg"));
	             ImageIO.write(bi1, "jpg", ops);         
	         } catch (IOException e) {
	             e.printStackTrace();
	         }
             System.out.println("图片已存入。");*/
	         
	            
	            
	            
 }


public void getDirectory (File file) {

	 File flist[] = file.listFiles();
	 if (flist == null || flist.length == 0) 
	 {
		 System.out.println("error\r\n"); 
	 }
	 for (File f : flist) {
	   if (f.isDirectory()) {
	     //这里将列出所有的文件夹
	     kus[ku1]=f.getAbsolutePath(); 
	     ku1++;
	     getDirectory(f);
	   } else {
	     //这里将列出所有的文件
		   kus[ku1]=f.getAbsolutePath(); 
		     ku1++;
	   }
	 }
}
 public double bl (String image,int t)
 {
	 int[] rgb = new int[3];
     File file = new File(image);
    BufferedImage bi = null;
     try {
        bi = ImageIO.read(file);
    } catch (IOException e) {
    
        e.printStackTrace();
    }
    int width = bi.getWidth();
    int height = bi.getHeight();
    int minX = bi.getMinX();
    int minY = bi.getMinY();
    for(int x = minX; x < width; x++) {
   	 for(int y = minY; y < height; y++){
            //获取包含这个像素的颜色信息的值, int型
            int pixel = bi.getRGB(x, y);
            //从pixel中获取rgb的值
            rgb[0] = (pixel & 0xff0000) >> 16; //r
            rgb[1] = (pixel & 0xff00) >> 8; //g
           rgb[2] = (pixel & 0xff); //b
   	 }
    }
           //System.out.println("x:"+x+"y:"+y);
           //System.out.println("r:"+rgb[0]+"g:"+rgb[1]+"b:"+rgb[2]);
    int a=(width-minX),b=(height-minY);
    int area1[] = new int [400];
    int area2[] = new int [400];
    int area3[] = new int [400];
    int area4[] = new int [400];
    int area5[] = new int [400];
    int area6[] = new int [2000];
    int pixel;
    int i=0,r=0;
    for(int x = (a/4)-10; x < (a/4)+10; x++) {
   	 for(int y = (b/4)-10; y < (b/4)+10; y++){
   		 pixel = bi.getRGB(x, y);
            //从pixel中获取rgb的值
            rgb[0] = (pixel & 0xff0000) >> 16; //r
            rgb[1] = (pixel & 0xff00) >> 8; //g
           rgb[2] = (pixel & 0xff); //b
   	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
   	area1[i]=fft2(x, y, r, 20, 20);
   	i++;
   	 }
   }
    i=0;
    for(int x = (a/4)-10; x < (a/4)+10; x++) {
   	 for(int y = (b*3/4)-10; y < (b*3/4)+10; y++){
   		 pixel = bi.getRGB(x, y);
            //从pixel中获取rgb的值
            rgb[0] = (pixel & 0xff0000) >> 16; //r
            rgb[1] = (pixel & 0xff00) >> 8; //g
           rgb[2] = (pixel & 0xff); //b
   	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
   	area2[i]=fft2(x, y, r, 20, 20);
   	i++;
   	 }
   }
    i=0;
    for(int x = (a*3/4)-10; x < (a*3/4)+10; x++) {
   	 for(int y = (b/4)-10; y < (b/4)+10; y++){
   		 pixel = bi.getRGB(x, y);
            //从pixel中获取rgb的值
            rgb[0] = (pixel & 0xff0000) >> 16; //r
            rgb[1] = (pixel & 0xff00) >> 8; //g
           rgb[2] = (pixel & 0xff); //b
   	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
   	area3[i]=fft2(x, y, r, 20, 20);
   	i++;
   	 }
   }
    i=0;
    for(int x = (a*3/4)-10; x < (a*3/4)+10; x++) {
   	 for(int y = (b*3/4)-10; y < (b*3/4)+10; y++){
   		 pixel = bi.getRGB(x, y);
            //从pixel中获取rgb的值
            rgb[0] = (pixel & 0xff0000) >> 16; //r
            rgb[1] = (pixel & 0xff00) >> 8; //g
           rgb[2] = (pixel & 0xff); //b
   	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
   	area4[i]=fft2(x, y, r, 20, 20);
   	i++;
   	 }
   }
    i=0;
    for(int x = (a/2)-10; x < (a/2)+10; x++) {
   	 for(int y = (b/2)-10; y < (b/2)+10; y++){
   		  pixel = bi.getRGB(x, y);
            //从pixel中获取rgb的值
            rgb[0] = (pixel & 0xff0000) >> 16; //r
            rgb[1] = (pixel & 0xff00) >> 8; //g
           rgb[2] = (pixel & 0xff); //b
   	r=(rgb[0]+rgb[1]+rgb[2])/3;	 
   	area5[i]=fft2(x, y, r, 20, 20);
   	i++;
   	 }
   }
    for (i=0;i<400;i++)
    {
    	area6[i]=area1[i];	
    	System.out.println("pic"+t+":"+area6[i]);
    	
    }
    for (i=400;i<800;i++)
    {
    	area6[i]=area2[i-400];	
    	System.out.println("pic"+t+":"+area6[i]);
    	
    }
    for (i=800;i<1200;i++)
    {
    	area6[i]=area3[i-800];	
    	System.out.println("pic"+t+":"+area6[i]);
    	
    }
    for (i=1200;i<1600;i++)
    {
    	area6[i]=area4[i-1200];	
    	System.out.println("pic"+t+":"+area6[i]);
    	
    }
    for (i=1600;i<2000;i++)
    {
    	area6[i]=area5[i-1600];	
    	System.out.println("pic"+t+":"+area6[i]);
    	
    }
    
    
    double xs=0;
    for (i=0;i<2000;i++)
    {xs+=Math.pow((area6[i]-area7[i]),2);}
    xs=Math.sqrt(xs);
    //System.out.println("xsd"+t+":"+xs);
   
   
   
   
   
  return xs; 
 }
 
 public int fft2 (int x,int y,int h,int sizex,int sizey)
	{
	  int i=0,j=0,fi=0;
	  double f=0,R=0,I=0;
	  for (i=0;i<sizex;i++)
		{
			for (j=0;j<sizey;j++)
			{
			R+=h*Math.cos(-2*Math.PI*((Math.pow(x, 2)/sizex)+(Math.pow(y, 2)/sizey)));	
			}
		}    
	  for (i=0;i<sizex;i++)
		{
			for (j=0;j<sizey;j++)
			{
			I+=h*Math.sin(-2*Math.PI*((Math.pow(x, 2)/sizex)+(Math.pow(y, 2)/sizey)));	
			}
		}  
	  f=Math.sqrt(Math.pow(R, 2)+Math.pow(I, 2));
	  fi=(int)(f+0.5);
   return fi;  
	}
 
 
 
 
 
 
}
