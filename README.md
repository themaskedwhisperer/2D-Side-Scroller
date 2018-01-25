# 2D-Side-Scroller

(from 2015) https://itp.nyu.edu/classes/creativecomputing-spring2015/author/sss639/  Java

"Very incomplete, frustrating, semi-broken (keep getting null errors each time I attempt to insert the spritesheet and which frames to animate) code. I have a bajillion codes I’ve been trying to make use of and even tried examples I seen online to see how I could create a functional code based with the knowledge I’ve learned in this course. This is my best attempt at it right now."

public class HeroineGame

  private static final String TAG = HeroineGame.class.getSimpleName();

  private Bitmap bitmap;    // the animation sequence
  private Rect sourceRect;  // the rectangle to be drawn from the animation bitmap
  private int frameNr;    // number of frames in animation
  private int currentFrame;  // the current frame
  private long frameTicker;  // the time of the last frame update
  private int framePeriod;  // milliseconds between each frame (1000/fps)

  private int spriteWidth;  // the width of the sprite to calculate the cut out rectangle
  private int spriteHeight;  // the height of sprite

  private int x;        // the X coordinate of the object (top left of the image)
  private int y;        // the Y coordinate of the object (top left of the image)

}

public void update(long gameTime) {
  if (gameTime > frameTicker + framePeriod) {
    frameTicker = gameTime;
    // increment the frame
    currentFrame++;
    if (currentFrame >= frameNr) {
      currentFrame = 0;
    }
  }
  // define the rectangle to cut out sprite
  this.sourceRect.left = currentFrame * spriteWidth;
  this.sourceRect.right = this.sourceRect.left + spriteWidth;
}

public void update() {
  heroine.update(System.currentTimeMillis());
}
public void draw(Canvas canvas) {
    // where to draw the sprite
    Rect destRect = new Rect(getX(), getY(), getX() + spriteWidth, getY() + spriteHeight);
    canvas.drawBitmap(bitmap, sourceRect, destRect, null);
  }
  
  private HeroineGame heroine;

  public MainGamePanel(Context context) {
   

    // create spirte and load hopefully
    heroine = new HeroineGame(
        BitmapFactory.decodeResource(getResources(), R.drawable.SpriteSheet1.png)
        , 10, 50  // initial position
        , 30, 47  // width and height of sprite
        , 5, 5);  // FPS and number of frames in the animation

    // create the game loop thread
    thread = new MainThread(getHolder(), this);

}

public void draw(Canvas canvas) {
  // where to draw the sprite
  Rect destRect = new Rect(getX(), getY(), getX() + spriteWidth, getY() + spriteHeight);
  canvas.drawBitmap(bitmap, sourceRect, destRect, null);
  canvas.drawBitmap(bitmap, 20, 150, null);
  Paint paint = new Paint();
  paint.setARGB(50, 0, 255, 0);
  canvas.drawRect(20 + (currentFrame * destRect.width()), 150, 20 + (currentFrame * destRect.width()) + destRect.width(), 150 + destRect.height(),  paint);
}


1/12/18 - Maybe I should load the assets and new models and it would help it function?
