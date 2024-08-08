import java.awt.*;
import java.awt.geom.Path2D;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.*;

public class HappyBDayBitisha extends JPanel implements ActionListener {
    private static final long serialVersionUID = 1L;
    private float scale = 1.0f;
    // here \u2764 = heartshapes
    private String message = "\u2764 Enter Your Messages \u2764";
    private String message1 = "\u2764 Enter Your Messages.\u2764";
    private String message2 = "\u2764 Enter Your Messages.\u2764";
    private String message3 = "\u2764 Enter Your Messages.\u2764";
    private Color[] colors = {Color.ORANGE , Color.BLUE,Color.RED , Color.GREEN, Color.MAGENTA,  Color.CYAN, Color.PINK ,Color.YELLOW};
    private int colorIndex = 0;

    public HappyBDayBitisha() {
        // this timer adjust the time of heart movement
        Timer heartTimer = new Timer(70, e -> {
            scale += 0.05f;
            if (scale > 2.0f) {
                scale = 1.0f;
            }
            repaint();
        });
        heartTimer.start();

        Timer textColorTimer = new Timer(1000, this);
        textColorTimer.start();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        Graphics2D g2d = (Graphics2D) g;
        g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
        g2d.setColor(Color.RED);
        int width = getWidth();
        int height = getHeight();
        // you can adjust the scale of heart 
        Path2D heart = createHeartPath(width / 2, height / 2.5, 65 * scale);
        g2d.fill(heart);

        g.setFont(new Font("Serif", Font.BOLD, 24));
        g.setColor(colors[colorIndex]);
        g.drawString(message, 32, 150);
        g.drawString(message1, 30, 180);
        g.drawString(message2, 30, 210);
        g.drawString(message3, 30, 240);
    }

    private Path2D createHeartPath(double x, double y, double size) {
        Path2D path = new Path2D.Double();
        // you can adjust the movement of heart 
        path.moveTo(x, y);
        path.curveTo(x + size / 2, y - size, x + size * 2, y + size / 3, x, y + size);
        path.curveTo(x - size * 2, y + size / 3, x - size / 2, y - size, x, y);
        return path;
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        colorIndex = (colorIndex + 1) % colors.length;
        repaint();
    }

    public static void main(String[] args) {
        JFrame frame = new JFrame("🥰Happy BirthDay Madamji🥰");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(550, 400);
        
        HappyBDayBitisha panel = new HappyBDayBitisha();
        panel.setBackground(Color.BLACK);  

        frame.add(panel);
        frame.setVisible(true);
    }
}
