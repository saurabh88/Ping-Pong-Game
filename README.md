Ping-Pong-Game
==============

Please update the code ,add new features and send me back.It's a code for J2ME game application





import javax.microedition.lcdui.*;
import javax.microedition.midlet.*;
import javax.microedition.lcdui.game.*;

public class HelloMIDlet extends MIDlet{
  
    PongCanvas pongCanvas;
  
    public HelloMIDlet() {
    pongCanvas=new PongCanvas(this);  
    }
  
    public void startApp() {
     
    Display.getDisplay(this).setCurrent(pongCanvas);;
    }
    
    public void pauseApp() {}
  
    public void destroyApp(boolean unconditional) {}
}
class PongCanvas extends Canvas implements Runnable,CommandListener{
  MIDlet midlet; 

	Command exitCommand;      
	Command helpCommand;
	Command newCommand; 

	int x_pos2 = 1;
	int y_pos2 = 1;
	int radius2 = 10;
	int x=240;
	int y=250;
	int x2=10;
	int y2=10;
	int x4=100;
	int y4=250;
	int x_speed2,y_speed2;
	
	static Image dbImage;
	Graphics dbg;

    public PongCanvas(MIDlet midlet_){

    midlet=midlet_;
    Display d=Display.getDisplay(midlet);
    exitCommand=new Command("Exit",Command.BACK,2);
    newCommand=new Command("New Game",Command.BACK,2);
    helpCommand=new Command("Help",Command.BACK,2);

    new Thread(this).start();

    addCommand(exitCommand);
    addCommand(newCommand);
    addCommand(helpCommand);
    setCommandListener(this);
    repaint();
    }

    public void keyPressed(int code){
    int game=getGameAction(code);

    switch(game){
    case Canvas.UP:
      
      break;
    case Canvas.DOWN:
      break;
    case Canvas.LEFT:
	x4=x4-15;
      break;
    case Canvas.RIGHT:
        x4=x4+15;
      break;
    }
    }

    public void keyRepeated(int code){
    int game=getGameAction(code);

    switch(game){
    case Canvas.UP:
      
      break;
    case Canvas.DOWN:
      break;
    case Canvas.LEFT:
	x4=x4-15;
      break;
    case Canvas.RIGHT:
        x4=x4+15;
      break;
    }
    }

    public void commandAction(Command c, Displayable d) {
    if (c == exitCommand) {
      midlet.notifyDestroyed();

    }
    else if(c == newCommand){
    x_speed2=2;
    y_speed2=2;
    x_pos2=40;
    y_pos2=50;
    radius2= 10;
    }
}
	public void run(){
		Thread.currentThread().setPriority(Thread.MIN_PRIORITY);
		while(true)
		{
			repaint();
			try{
				Thread.sleep(5);
			}catch(InterruptedException e){}

		if (x_pos2 > 230-10-radius2)
		{

	    	// Change direction of ball movement
	    x_speed2 = -3; 

		}
		else if(x_pos2 < radius2+10)
		{

	    	// Change direction of ball movement
		    x_speed2 = 3; 

		}
		else if(y_pos2 > y-10-radius2 && (x_pos2 > x4 && x_pos2<x4+70))
		{

	    	// Change direction of ball movement
		    y_speed2 = -3; 
		
		}
		else if((x_pos2 < x4 || x_pos2>x4+70) && y_pos2 > y-10-radius2)
		{
			y_speed2=0;
			x_speed2=0;
  			radius2=0;
		}
		else if (y_pos2 < radius2+10)
		{

	    	// Change direction of ball movement
		    y_speed2=3; 

		}
		
		x_pos2=x_pos2+x_speed2;
		y_pos2=y_pos2+y_speed2;
		
	}
	//Thread.currentThread().setPriority(Thread.MAX_PRIORITY);
} 

	public void update (Graphics g)
	{

	    // initialize buffer
    		if (dbImage == null)
    		{
       			 dbImage=Image.createImage(250,250);
  		         dbg = dbImage.getGraphics();
    		}

		    // clear screen in background
    	dbg.setColor (255,20,255);
    	dbg.fillRect (0, 0, 250, 250);

	    // draw elements in background
    	dbg.setColor (255,255,255);
	    paint (dbg);

	    // draw image on the screen
    	g.drawImage (dbImage, 0, 0, 0);
	}
	public void paint(Graphics g){
		
		g.setColor(0,2,200);
		g.fillRect(0,0,240,250);
		g.setColor(200,255,90);
		g.fillRect(10,10,220,230);
		
		g.setColor(0,250,0);
		g.setColor(255,0,0);
		//g.drawString("Created by SAURABH",20,40,g.TOP|g.LEFT);
		
		g.setColor(0,0,0);
		g.drawLine(0,y,x,y);
		g.drawLine(0,0,x,0);
		g.drawLine(0,0,0,y);
		g.drawLine(x,0,x,y);
		g.drawLine(x-x2,0+y2,x-x2,y-y2);
		g.drawLine(0+x2,y-y2,x-x2,y-y2);
		g.drawLine(x-x2,y-y2,x,y);
		g.drawLine(0,y,x2,y);
		g.drawLine(x2,y2,0,0);
		g.drawLine(x2,y2,x2,y-y2);
		g.drawLine(x2,y2,x-x2,y2);
		g.drawLine(x,0,x-x2,y2);
		g.drawLine(x2,y-y2,0,y);
		g.drawLine(x2/2,y-(y2/2),x2/2,y2/2);
		g.drawLine(x2/2,y2/2,x-(x2/2),y2/2);
		g.drawLine(x-x2/2,y-y2/2,x-x2/2,y2/2);
			
		g.setColor(255,0,0);
		g.fillArc(x_pos2 - radius2, y_pos2 - radius2, 2 * radius2, 2 * radius2,0,360);
		g.setColor(255,255,255);
		g.fillArc(x_pos2 - radius2+10, y_pos2+10 - radius2, 6,6,0,360);
			
		g.setColor(200,24,50);
		g.fillRoundRect(x4,235,70,10,20,20);
		if(radius2==0)
		{
                g.drawString("GAME OVER",60,60,g.TOP|g.LEFT);
		}	
	}
} 