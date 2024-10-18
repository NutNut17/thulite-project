---
title: "Java AWT"
description: "Simple Java GUI"
summary: ""
date: 2024-10-09T17:04:51+08:00
lastmod: 2024-10-09T17:04:51+08:00
draft: false
weight: 202
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---
This is just a demonstration of how to make GUI using java. However, the tools used in this page is very simple and not quite modern.

#### AWT (Abstract Windowing Toolkit)

Below is a code to make windows using AWT

```java
import java.awt.*;

public class T1 {
    static Frame fm = new Frame("Frame Test");
    static Label lb = new Label();
    static Button bn = new Button("Press");
    static Checkbox cb1 = new Checkbox("Selection 1", true);
    static Checkbox cb2 = new Checkbox("Selection 2", false);
    static Checkbox cb3 = new Checkbox("Selection 3");
    static Checkbox cb4 = new Checkbox("Selection 4", true);
    static Checkbox cb5 = new Checkbox("Selection 5", true);
    static TextField tf1 = new TextField("Text Field 1");
    static TextField tf2 = new TextField("Text Field 2");
    static TextArea ta = new TextArea("demo", 10, 10, TextArea.SCROLLBARS_VERTICAL_ONLY);

    public static void main(String args[]) {
        fm.setLayout(null); // Must reset the layout to enable object to be placed at frame manually
        fm.setSize(500, 500);
        fm.setLocation(-6, 0); // x = -6 to stick the left edge, default(0, 0)
        fm.setBackground(Color.pink); // Default: White

    lb.setText("This is a label");
        lb.setLocation(50, 50); // Location relative to the frame
        lb.setSize(150, 30);
        lb.setBackground(Color.white);
        lb.setAlignment(Label.CENTER);
        lb.setForeground(Color.DARK_GRAY); // Text Color
        Font ft = new Font("Serief", Font.ITALIC + Font.BOLD, 18);
        lb.setFont(ft);

    bn.setSize(150, 30);
        bn.setLocation(50, 90);
        // bn.setBounds(50, 90, 150, 30); // We can use this as alternative

    cb1.setBounds(50, 130, 150, 10);
        cb2.setBounds(50, 150, 150, 10);
        cb3.setBounds(50, 170, 150, 10);
        cb4.setBounds(50, 190, 150, 10);
        cb5.setBounds(50, 210, 150, 10);
        CheckboxGroup gp = new CheckboxGroup(); // Grouped Checkbox may only have one true
        cb4.setCheckboxGroup(gp);
        cb5.setCheckboxGroup(gp);

    tf1.setBounds(50, 230, 150, 20);
        tf2.setBounds(50, 260, 150, 20);
        tf1.setEditable(false);
        tf2.setEchoChar('*');// Commonly for password input

    ta.setBounds(50, 290, 150, 100);

    fm.add(lb);
        fm.add(bn);
        fm.add(cb1);
        fm.add(cb2);
        fm.add(cb3);
        fm.add(cb4);
        fm.add(cb5);
        fm.add(tf1);
        fm.add(tf2);
        fm.add(ta);
        fm.setVisible(true);
    }
}
```

* AWT Layouts - do frm.setLayout(layoutInstance) to apply layout
* Border Layout - Adds components to 5 direction of the layout, EAST, SOUTH, WEST, NORTH and CENTER

```java
BorderLayout border = new BorderLayout(int hgap, int vgap);
frm.setLayout(border);
frm.add(new Button("North"),border.NORTH);
```

* Card Layout - Stack cards(components)

```java
CardLayout card = new CardLayout(int hgap, int vgap);
frm.setLayout(card);
frm.add(new Button("Button 1"),"c1");
frm.add(new Button("Button 2"),"c2");
...
card.show(frm,"c1");    // Put c1 on top of stack to be showed
```

* Flow Layout - Components are flexible and moves from left to right, up to down

```java
FlowLayout flow = new FlowLayout(int align, int hgap, int vgap);
frm.setLayout(flow);
frm.add(new Button("Button 1"));
```

* Grid Layout - Add grid to the frame

```java
GridLayout grid = new GridLayout(int rows, int cols, int hgap, int vgap);
frm.setLayout(grid);
loop(){ frm.add(new Button("Button i")) };
```

* Using Panels - Layouts are implmented on the whole window. If we want to splits the layout we can use panel to act as container

```java
// A code for simple calculator frame

static Frame frm = new Frame();
static Panel pnl = new Panel(new GridLayout(3, 3));
static Label lab = new Label("0. ", Label.RIGHT);
public static void main(String args[]){
    frm.setLayout(null);    // Clear layout first
    frm.setSize(200,150);
    frm.setResizable(false);
    lab.setBounds(20, 30, 120, 20);
    lab.setBackground(new Color(240, 220, 190));
    pnl.setBounds(20, 60, 120, 80);
    for(int i = 0; i < 9; i++)
        pnl.add(new Button(Integer.toString(i)));
    frm.add(lab);
    frm.add(pnl);
    frm.setVisible(true);
}
```

#### Swing

A swing is a floating window that is better than frame, because the contents of swing can adjust based on the floating window
size. JFrame is the top-level container for swing. It is a class just like JDialog, JWindow but JFrame is used for commonly
seen floating window. We mmust import javax.swing.* library to use swing.

JFrame() or JFrame(String title)    // Create JFrame class for a floating window (Top-Level)

Container contentPane = frame.getContentPane()    // Get content panel of a floating window (Secondary-Level)

JScrollPane and Jpanel is similar, they are the subcontainer of a content pane (Tertiary-Level) can be used to organize
different part of a content pane. JScrollPane has an addition scrolling feature.

Layout Manager - BorderLayout, FlowLayout, GridLayout,

Below is an example of how swing is made:

```java
import java.awt.*;
import javax.swing.*;

public class Test {
    public static void main(String[] args) {
        JFrame frm = new JFrame("Name of Floating Window");
        frm.setLayout(null);
        Container cp = frm.getContentPane();
        cp.setLayout(new BorderLayout()); // BorderLayout puts objects on N, E, S, W and CENTER
        JPanel p1 = new JPanel(new WrapLayout(FlowLayout.CENTER));

    JLabel lbl = new JLabel("This is a label");
        p1.add(lbl);

    JButton btn1 = new JButton("Press Doge", new ImageIcon(".\\doge.jpg"));
        p1.add(btn1);

    JTextField txt1 = new JTextField("Text", 10);
        p1.add(txt1);

    JTextField txt2 = new JPasswordField("Text", 10);
        p1.add(txt2);

    JCheckBox c1 = new JCheckBox("A"), c2 = new JCheckBox("B");
        p1.add(c1);
        p1.add(c2);

    JRadioButton r1 = new JRadioButton("a"), r2 = new JRadioButton("b");
        p1.add(r1);
        p1.add(r2);
        ButtonGroup bgroup1 = new ButtonGroup();
        bgroup1.add(r1);
        bgroup1.add(r2);

    String[] s = { " 1 ", " 2 ", " 3 " };
        JList`<String>` list = new JList `<String>`(s);
        list.setBorder(BorderFactory.createTitledBorder("N"));
        p1.add(list);

    JComboBox`<String>` combo = new JComboBox `<String>`(s);
        combo.addItem(" 4 ");
        combo.setBorder(BorderFactory.createTitledBorder("N"));
        p1.add(combo);

    JTextArea area = new JTextArea(10, 30);
        area.append("Comments:\n");
        p1.add(area);

    JMenuBar MBar = new JMenuBar();
        JMenu thefile = new JMenu("File");
        JMenuItem newf = new JMenuItem("New");
        JMenuItem open = new JMenuItem("Open");
        JMenuItem close = new JMenuItem("Close");
        JMenuItem quit = new JMenuItem("Exit");
        open.setMnemonic('O');
        thefile.add(newf);
        thefile.add(open);
        thefile.add(close);
        thefile.addSeparator();
        thefile.add(quit);
        MBar.add(thefile);
        frm.setJMenuBar(MBar);

    JInternalFrame internalFrame = new JInternalFrame("Internal Frame 1", true,
                true, true, true);
        internalFrame.setLocation(20, 400);
        internalFrame.setSize(200, 200);
        internalFrame.setVisible(true);
        Container icontentPane = internalFrame.getContentPane();
        JTextArea textArea = new JTextArea();
        JButton b = new JButton("Internal Frame Button");
        icontentPane.add(textArea, "Center");
        icontentPane.add(b, "South");
        // JDesktopPane desktopPane = new JDesktopPane();
        // desktopPane.add(internalFrame);
        // cp.add(desktopPane, BorderLayout.SOUTH);
        cp.add(internalFrame, BorderLayout.SOUTH);

    String[] heading = new String[] { "序號", "學號", "系所", "姓名" };
        String[][] data = new String[][] {
                { "1", "92610066", "資訊工程系", "王小明" },
                { "2", "92610067", "資訊工程系", "陳大氣" },
                { "3", "92660059", "企業管理系", "楊宗藩" },
                { "4", "92760101", "電子工程", "李明雄" }
        };

    JTable table = new JTable(data, heading);
        JScrollPane scrollPane2 = new JScrollPane(table);
        scrollPane2.setPreferredSize(new Dimension(1000, 300));
        // If JPanel is used instead of JScrollPane, the header will not be displayed
        cp.add(scrollPane2, BorderLayout.AFTER_LAST_LINE);

    JScrollPane scrollPane = new JScrollPane(p1, ScrollPaneConstants.VERTICAL_SCROLLBAR_ALWAYS,
                ScrollPaneConstants.HORIZONTAL_SCROLLBAR_NEVER);
        scrollPane.setPreferredSize(new Dimension(1000, 300));
        cp.add(scrollPane);

    frm.setLocation(-6, 0);
        frm.setSize(1000, 700);
        frm.setVisible(true);
        frm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}

// WrapLayout source
// [https://gist.github.com/jirkapenzes/4560255#file-wraplayout-java](https://gist.github.com/jirkapenzes/4560255#file-wraplayout-java)
class WrapLayout extends FlowLayout {
    // private Dimension preferredLayoutSize;

    public WrapLayout() {
        super();
    }

    public WrapLayout(int align) {
        super(align);
    }

    public WrapLayout(int align, int hgap, int vgap) {
        super(align, hgap, vgap);
    }

    @Override
    public Dimension preferredLayoutSize(Container target) {
        return layoutSize(target, true);
    }

    @Override
    public Dimension minimumLayoutSize(Container target) {
        Dimension minimum = layoutSize(target, false);
        minimum.width -= (getHgap() + 1);
        return minimum;
    }

    private Dimension layoutSize(Container target, boolean preferred) {
        synchronized (target.getTreeLock()) {
            int targetWidth = target.getSize().width;

    if (targetWidth == 0)
                targetWidth = Integer.MAX_VALUE;

    int hgap = getHgap();
            int vgap = getVgap();
            Insets insets = target.getInsets();
            int horizontalInsetsAndGap = insets.left + insets.right + (hgap * 2);
            int maxWidth = targetWidth - horizontalInsetsAndGap;

    Dimension dim = new Dimension(0, 0);
            int rowWidth = 0;
            int rowHeight = 0;

    int nmembers = target.getComponentCount();

    for (int i = 0; i < nmembers; i++) {
                Component m = target.getComponent(i);

    if (m.isVisible()) {
                    Dimension d = preferred ? m.getPreferredSize() : m.getMinimumSize();

    if (rowWidth + d.width > maxWidth) {
                        addRow(dim, rowWidth, rowHeight);
                        rowWidth = 0;
                        rowHeight = 0;
                    }

    if (rowWidth != 0) {
                        rowWidth += hgap;
                    }

    rowWidth += d.width;
                    rowHeight = Math.max(rowHeight, d.height);
                }
            }

    addRow(dim, rowWidth, rowHeight);

    dim.width += horizontalInsetsAndGap;
            dim.height += insets.top + insets.bottom + vgap * 2;

    Container scrollPane = SwingUtilities.getAncestorOfClass(JScrollPane.class, target);
            if (scrollPane != null) {
                dim.width -= (hgap + 1);
            }

    return dim;
        }
    }

    private void addRow(Dimension dim, int rowWidth, int rowHeight) {
        dim.width = Math.max(dim.width, rowWidth);

    if (dim.height > 0) {
            dim.height += getVgap();
        }

    dim.height += rowHeight;
    }
}
```

#### Event Handling

When an defined event is triggered, the implementation of specific interface will create an object of the event type and the
event listener will handle the case when the event object is listened. Since the interface will be inplemented, we need to
define the abstract method explicitly.

```java
import java.awt.event.*;
public class xxxx implements ActionListener
{
  public void actionPerformed(ActionEvent e)
  {
    JOptionPane.showMessageDialog(null,"Message","Title",JOptionPane.WARNING_MESSAGE);
  }
}
```

There is few ways to do it

- extends JFrame and implements listener on the file class
- create a class either in the file class or outside of the file class and implement listener. Then create the class in
  addActionListener. For example: btn.addActionListener(new Actlis())
- declare listener in addActionListener. For example btn.addActionListener(new ActionListener(){public void
  actionPerformed(ActioneEvent e){ JOptionPane.showMessageDialog(...);}});

btn.addActionListener(frm); // btn is the source, frm is the listener which implements ActionListener
public void actionPerformed(ActioneEvent e){...} // override event handling
object e.getSource() // Get the source of event
object e.isSelected() // Check if the JRadioButton or the JCheckBox is checked

Below are the event types:

EventInterface(EventAdapter, this is the class version of interface), EventListener, EventMethod:

ActionEvent, ActionListener, actionPerformed(ActioneEvent e)
ItemEvent, ItemListener, itemStateChanged(ItemEvent e)
TextEvent, TextListener, textStateChanged(TextEvent e)
AdjustmentEvent, AdjustmentListener, adjustmentStateChanged(AdjustmentEvent e)
KeyEvent, KeyListener, key Typed/Pressed/Released (KeyEvent e)
MouseEvent, MouseListener, mouse Clicked/Entered/Exited/Pressed/Released/Dragged/Moved (MouseEvent e)
WindowEvent, WindowListener, window Activated/Closed/Closing/Deactivated/Deiconified/Iconified/Opened (WindowEvent e)

```java
static class KeyLis implements KeyListener // For text
{
  public void keyPressed(KeyEvent e)
  {
    if(e.isActionKey())
      lab.setText("Action key is pressed\n");
    else lab.setText(Character.toString(e.getKeyChar())+" is pressed\n");
    //if(e.getKeyCode() == KeyEvent.VK_ENTER) //判斷是否按Enter鑑
  }
  public void keyReleased(KeyEvent e){}
  public void keyTyped(KeyEvent e){}
}

static class actLis implements ItemListener // For combobox
{
  public void itemStateChanged(ItemEvent e) {
     if (e.getStateChange()== ItemEvent.SELECTED)
         JOptionPane.showMessageDialog(null, Integer.toString(combo1.getSelectedIndex()) +     combo1.getSelectedItem());
  }
}
```

#### JColorChoser

```java
import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

public class Test {
    static JFrame frm = new JFrame("JColorChoser");
    static Container cp = frm.getContentPane();
    static JButton btn = new JButton("Get Color");
    static Color color;

    public static void main(String args[]) {
        cp.setLayout(new BorderLayout());
        cp.add(btn, BorderLayout.SOUTH);
        btn.addActionListener(new Actlis());
        cp.setBackground(Color.YELLOW);
        frm.setSize(200, 150);
        frm.setVisible(true);
        frm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    static class Actlis implements ActionListener {
        public void actionPerformed(ActionEvent e) {
            color = JColorChooser.showDialog(frm, "JColorChoser", Color.pink);
            cp.setBackground(color);
        }
    }
}
```
