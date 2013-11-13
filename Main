import java.awt.Canvas;
import java.awt.Dimension;
import java.awt.Graphics;
import java.awt.image.BufferStrategy;
import java.awt.image.BufferedImage;
import java.awt.image.DataBufferInt;

import javax.swing.JFrame;

public class Main extends Canvas implements Runnable {
	private static final long serialVersionUID = 1L;
	
	public final int WIDTH = 520;
	public final int HEIGHT = (WIDTH * 9) / 12;

	BufferedImage bimg = new BufferedImage(WIDTH, HEIGHT, BufferedImage.TYPE_INT_RGB);
	int[] pixels = ((DataBufferInt) bimg.getRaster().getDataBuffer()).getData();

	public boolean running;

	public Main() {
		Dimension size = new Dimension(WIDTH, HEIGHT);
		this.setSize(size);
	}

	public void start() {
		running = true;
		new Thread(this).start();
	}

	@Override
	public void run() {
		long now = 2;
		while (running) {
			now += 10;
			render(now);
			logic();
		}
	}

	private void render(long now) {
		for (int x = 0; x < WIDTH; x++) {
			for (int y = 0; y < HEIGHT; y++) {
				pixels[x + y * WIDTH] = (int) now + x * y;
			}
		}
		BufferStrategy bs = this.getBufferStrategy();
		if (bs == null) {
			if (this.getFocusCycleRootAncestor() != null)
				this.createBufferStrategy(3);
			return;
		}

		Graphics g = bs.getDrawGraphics();

		g.drawImage(bimg, 0, 0, this.getWidth(), this.getHeight(), null);

		g.dispose();
		bs.show();
	}

	public void logic(){
		
	}
	
	public static void main(String[] args) {
		Main game = new Main();
		JFrame frame = new JFrame();
		frame.add(game);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.setResizable(false);

		frame.pack();
		frame.setVisible(true);
		game.start();
	}
}
