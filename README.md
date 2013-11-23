CirkelUppgift
=============

CirkelUppgift av Leo Ahnstedt

package 
{
	import flash.display.Sprite;
	import flash.events.Event;
	import flash.events.KeyboardEvent;
	import flash.events.MouseEvent;
	import flash.events.TextEvent;
	import flash.sampler.NewObjectSample;
	import flash.text.TextField;
	import flash.text.TextFormat;
	import flash.ui.Keyboard;
	
	/**
	 * ...
	 * @author Leo
	 */
	public class Main extends Sprite 
	{
		
		public var circleArray:Array = new Array();
		public const circleX:int = 20;
		public const circleY:int = 20;
		public var scoreBoxSprite:Sprite = new Sprite();
		public var scoreBoxText:TextField = new TextField();
		public var score:int;
		public var circleAmount:int = 20;
		
		public var format:TextFormat = new TextFormat();
		public var format2:TextFormat = new TextFormat();
		
		public var startBoxText:TextField = new TextField();
		public var gameStarted:Boolean = false;

		
		public function Main():void 
		{
			if (stage) init();
			else addEventListener(Event.ADDED_TO_STAGE, init);
		}
		
		private function init(e:Event = null):void 
		{
			removeEventListener(Event.ADDED_TO_STAGE, init);
			// entry point
			stage.addEventListener(KeyboardEvent.KEY_DOWN, spawnCircles);
			
			// Variables
			scoreBoxSprite.graphics.beginFill(0x0000A0);
			scoreBoxSprite.graphics.drawRect(0, 0, 200, 70);
			addChild(scoreBoxSprite);
			scoreBoxText.text = "Score: " + score;
			scoreBoxText.x = 20;
			scoreBoxText.y = 7;
			format.size = 43;
			format.italic = true;
			scoreBoxText.setTextFormat(format);
			scoreBoxText.width = 200
			scoreBoxText.textColor = (0xFFFFFF)
			addChild(scoreBoxText);
			
			startBoxText.text = "Press SPACE to start!";
			startBoxText.x = 200;
			startBoxText.y = 250;
			startBoxText.width = 500;
			format2.size = 43;
			format2.bold = true;
			startBoxText.setTextFormat(format2);
			addChild(startBoxText);
			
			
		}
		// Draw Circles Function
		public function spawnCircles(e:KeyboardEvent):void
			{
			switch (e.keyCode)
				{
					case Keyboard.SPACE:
					for (var i:int = 0; i < 20; i++) 
					{
						var circle =  new Sprite();
						startBoxText.text = " ";
						circle.graphics.beginFill(Math.random() * 0xffffff);
						circle.graphics.drawCircle(25, 25, 25);
						circle.graphics.endFill();
						circle.x = i+350 * Math.random() * 2;
						if (circle.x >= 800)
						{
							circle.x - 200;
						}
						if (circle.x <= 0)
						{
							circle.x + 200;
						}
						circle.y = i+250 * Math.random() * 2;
						if (circle.y >= 600)
						{
							circle.y - 200;
						}
						if (circle.y <= 0)
						{
							circle.y + 200;
						}
						if (circle.x <= 225 && circle.y <= 95)
						{
							circle.x = i + 350 * Math.random() * 2;
							circle.y = i + 250 * Math.random() * 2;
						}
						if (i == 1)
						{
							score++
						}
						addChild(circle);
						circleArray.push(circle);
							
						circleAmount -= 1;
						
						circle.addEventListener(MouseEvent.CLICK, deleteCircle);
						
						
					}
					
				}
			
			}
			// Delete Circle Function
			public function deleteCircle(e:MouseEvent):void
			{
				e.target.y -= 1000;
				if (Math.round(Math.random() * 20) == 10)
				{
					score -= 1;
					
				}
				scoreBoxText.text = "Score: " + score;
				format.size = 43;
				format.italic = true;
				scoreBoxText.setTextFormat(format);
				scoreBoxText.width = 200
				if (circleAmount >= 0)
				{
					score++;
				}	
			}	
			}
	}
}
}
