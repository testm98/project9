///Project #9 // squids.jave ///
///Matthew Testa///

int many=5;
Squid school[]= new Squid[many];
String names[]= { "one", "two", "three", "four", "five" };
float spacing;

int several=4;
Boat fleet[]= new Boat[several];
String title []= { "Boat one", "Boat two", "Boat three", "Boat four" };
float seperate;

float surface;
float moonX=0, moonY=100;
int score=0;

//// SETUP: SIZE AND RESET ////
void setup() {
  size(950, 600);
  spacing= width/( many+1 );
  seperate= width/( several+2 );
  reset();
}
  
  void reset() {
    surface= random( height/4, height/2 );
    moonY= surface/3;
    moonY= random( 200, surface+150);
    //squids//
    float x= spacing;
    for ( int i=0; i<many; i++ ) {
      school[i]= new Squid( names[i], x );
      x += spacing;
    }
  
    //boats//
    float sp= seperate;
    for ( int i=0; i<several; i++ ) {
      fleet[i]= new Boat();
      x += seperate;
    }
  }

void draw() {
  scene();
  action();
  show();
  move();
  fill(0);
  text( "Matt Testa: Squid 9", 10, height-10 );
  if ( score>0 ) text( "SCORE: "+score, width*5/8, 40 );
}
  
  void scene() {
  background( 80,120, 40 ); //sky//
  if ( moonX > width+100 ) {
    moonX = -50;
    moonY = random( 100, surface+50 );
  }
  moonX += 1;
  fill( 200,100,60 );
  ellipse( moonX, moonY-150*sin( PI * moonX/width), 30, 30 );
  //color of water//
  fill(70,180,80);
  noStroke();
  rect( 0,surface, width, height-surface );
  }
  
  void action() { //boat & squid movement//
  
 for ( int i=0; i<many; i++ ) {   //squid//
   school[i].move();
 }
 

 for (int i=0; i<several; i++ ) {
   fleet[i].move();
 }
  }
  

///Squids OBJECT//
class Squid {
  float x,y;
  float dx=0, dy=0;
  float w=50, h=50;
  int legs=8;
  String name="";
  float r,g,b;
  int count=0;
 
 ////COLOR AND NAME////
 Squid( String s, float x) {
 this.name= s;
 this.x=x;
 ///color///
 r= random ( 200,80 );
 g= random ( 160, 120 );
 b= random (120, 140 );
 }
 
 //start from bottom and set random speed//
 void bottom() {
   y= height - h*.75;
   dy= -random ( 0.1, 0.9 );
   legs= int( random ( 1, 10.9 ) );
 }
}

//////MOVE AND SHOW METHOD////
  void move() {
    x += dx;
    y += dy;
    if ( y>height ) {
      bottom();
    }
    else if ( y<surface ) {
      dy= -4 * dy; //descenting speed//
    }
  }
  
  ////DISPLAY SQUID//////
  void show() {
    fill( r,g,b );
    stroke( r,g,b );
    ellipse( x,y,w,h );
    rect( x-w/2, y, w, h/2 );
    fill(255);
    float blink=10;
    if ( y%100 > 80 ) blink=2;
    ellipse( x, y-h/4, 8, blink ); //eye//
    //next//
    fill( r,b,g );
    float legX= x-w/2, foot=0;  //legs and movement of legs//
    if ( dy<0 ) {
      foot=6;
      if( y%40 > 20 ) foot= -foot;
    }
    for ( int i=0; i<legs; i++ ) {
      line( legX, y+h/2, legX+foot, 20+y+h/2 );
      legX +=w / ( legs-1 );
    }
      
      strokeWeight( 2 );
      fill( 200, 200, 0 );
      text( name, x-w/2, y-6+h/2 );
      fill( 0 );
      text( legs, x+2-w/2, y+h/2 );
      fill( 190 );
      if ( count>0 ) text( count, x, y+h/2 );
  }
      ///return back to bottom if true//
      boolean hit( float xx, float yy ) {
        return dist( xx, yy, x,y ) < h;
      }
  
  
class Boat {    
   float x=0, y=surface, dx=5;
   int cargo=0, caught=0;
   void move() {
     int caught=0;
     for ( int i=0; i<many; i++ ); {
       /*if (school[i].hit( bounty.x, surface ) ) {
         caught += school[i].legs;
       }
     } */
     cargo += caught;
     //direction of movement//
     x += dx;
     if( caught>0 ) x += 2*dx;
     if ( x<0 ); {
       score += cargo;
       cargo = 0;
       dx = random (1, 4);
     }
     if ( x>width ); {
       dx = -random( 1, 4 ); //return with same speed//
     }
   }
  }
}

  //boat//
  void show() {
    fill( 200, 170, 190 );
    noStroke();
    rect( x, surface-20, 50, 20 );
    if (dx>0) triangle( x+50, surface, x+50, surface-20, x+70, surface-20 );
    else      triangle( x, surface, x,surface-20, x-20, surface-20);
    rect( x+12, surface-30, 25, 10 ); //cabin//
    rect( x+30, surface-40, 15, 30 ); //mast//
    //display name and cargo//
    fill( 255 );
    text( name, x+5, surface-10 );
    if( cargo>0 ) text( cargo, x+10, surface-20 );
  }
    
    
   
    
 
  
  

    
 
  
  
  
  


  
