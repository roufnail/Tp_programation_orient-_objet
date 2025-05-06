import java.util.Scanner;

class Point {
    private double x;
    private double y;
    
    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double getX() { return x; }
    public double getY() { return y; }
    
    public void translate(double dx, double dy) {
        x += dx;
        y += dy;
    }
    
    @Override
    public String toString() {
        return "(" + x + ", " + y + ")";
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Point point = (Point) obj;
        return Double.compare(point.x, x) == 0 && Double.compare(point.y, y) == 0;
    }
}

class Rectangle {
    protected Point bottomLeft;
    protected double width;
    protected double height;
    private static int nbr = 0;
    
    public Rectangle(Point p1, Point p2) {
        double x1 = Math.min(p1.getX(), p2.getX());
        double y1 = Math.min(p1.getY(), p2.getY());
        double x2 = Math.max(p1.getX(), p2.getX());
        double y2 = Math.max(p1.getY(), p2.getY());
        this.bottomLeft = new Point(x1, y1);
        this.width = x2 - x1;
        this.height = y2 - y1;
        nbr++;
    }
    
    public Rectangle(Point p, double width, double height) {
        this.bottomLeft = new Point(p.getX(), p.getY());
        this.width = width;
        this.height = height;
        nbr++;
    }
    
    public Rectangle(double x, double y, double width, double height) {
        this.bottomLeft = new Point(x, y);
        this.width = width;
        this.height = height;
        nbr++;
    }
    
    public double surface() {
        return width * height;
    }
    
    public void translate(double dx, double dy) {
        bottomLeft.translate(dx, dy);
    }
    
    public boolean contains(Point p) {
        return p.getX() >= bottomLeft.getX() && 
               p.getX() <= bottomLeft.getX() + width &&
               p.getY() >= bottomLeft.getY() && 
               p.getY() <= bottomLeft.getY() + height;
    }
    
    public boolean contains(Rectangle r) {
        return contains(r.bottomLeft) && 
               contains(new Point(r.bottomLeft.getX() + r.width, r.bottomLeft.getY() + r.height));
    }
    
    public boolean sameAs(Rectangle other) {
        return bottomLeft.equals(other.bottomLeft) && 
               width == other.width && 
               height == other.height;
    }
    
    public static int getNbr() {
        return nbr;
    }
    
    public static Rectangle hull(Rectangle[] rectangles) {
        if (rectangles == null || rectangles.length == 0) return null;
        
        double minX = rectangles[0].bottomLeft.getX();
        double minY = rectangles[0].bottomLeft.getY();
        double maxX = rectangles[0].bottomLeft.getX() + rectangles[0].width;
        double maxY = rectangles[0].bottomLeft.getY() + rectangles[0].height;
        
        for (int i = 1; i < rectangles.length; i++) {
            Rectangle r = rectangles[i];
            minX = Math.min(minX, r.bottomLeft.getX());
            minY = Math.min(minY, r.bottomLeft.getY());
            maxX = Math.max(maxX, r.bottomLeft.getX() + r.width);
            maxY = Math.max(maxY, r.bottomLeft.getY() + r.height);
        }
        
        return new Rectangle(minX, minY, maxX - minX, maxY - minY);
    }
    
    @Override
    public String toString() {
        return "Rectangle[bottomLeft=" + bottomLeft + ", width=" + width + ", height=" + height + "]";
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Rectangle rectangle = (Rectangle) obj;
        return Double.compare(rectangle.width, width) == 0 && 
               Double.compare(rectangle.height, height) == 0 && 
               bottomLeft.equals(rectangle.bottomLeft);
    }
}
class SlantedRectangle extends Rectangle {
    private double angle; // angle en radians
    
    public SlantedRectangle(Point p1, Point p2, double angle) {
        super(p1, p2);
        this.angle = angle;
    }
    
    public SlantedRectangle(Point p, double width, double height, double angle) {
        super(p, width, height);
        this.angle = angle;
    }
    
    public SlantedRectangle(double x, double y, double width, double height, double angle) {
        super(x, y, width, height);
        this.angle = angle;
    }
    
    public void rotate(double deltaAngle) {
        this.angle += deltaAngle;
    }
    
    @Override
    public boolean contains(Point p) {
        // Implémentation simplifiée - en réalité il faudrait faire une rotation inverse
        return super.contains(p);
    }
    
    @Override
    public boolean contains(Rectangle r) {
        if (r instanceof SlantedRectangle) {
            SlantedRectangle sr = (SlantedRectangle) r;
            return this.angle == sr.angle && super.contains(r);
        }
        return super.contains(r);
    }
    
    public boolean contains(SlantedRectangle sr) {
        return this.angle == sr.angle && super.contains(sr);
    }
    
    @Override
    public String toString() {
        return "SlantedRectangle[bottomLeft=" + bottomLeft + ", width=" + width + 
               ", height=" + height + ", angle=" + angle + "]";
    }
    
    @Override
    public boolean equals(Object obj) {
        if (!super.equals(obj)) return false;
        if (obj == null || getClass() != obj.getClass()) return false;
        SlantedRectangle that = (SlantedRectangle) obj;
        return Double.compare(that.angle, angle) == 0;
    }
}
class A {
    void f(A o) {
        System.out.println("void f(A o) dans A");
    }
    
    void f(B o) {
        System.out.println("void f(B o) dans A");
    }
}

class B extends A {
    void f(A o) {
        System.out.println("void f(A o) dans B");
    }
    
    void f(B o) {
        System.out.println("void f(B o) dans B");
    }
}

class C {
    char ch = 'C';
    char getCh() { return ch; }
}

class D extends C {
    char ch = 'D';
    char getCh() { return ch; }
}

public class HeritageMasquage {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("=== Programme sur l'héritage et le masquage de méthodes ===");
        System.out.println("Ce programme va vous guider à travers les exercices 1 à 13.");
        System.out.println("Vous allez entrer les données nécessaires pour chaque exercice.\n");
      
        // Exercice 1-4
      System.out.println("\n=== Exercices 1-4: Rectangles inclinés ===");
      System.out.println("Création d'un point, d'un rectangle et de rectangles inclinés...");
      
      System.out.print("Entrez les coordonnées du point (x y): ");
      double x = scanner.nextDouble();
      double y = scanner.nextDouble();
      Point p = new Point(x, y);
      
      System.out.print("Entrez les dimensions du rectangle (largeur hauteur): ");
      double width = scanner.nextDouble();
      double height = scanner.nextDouble();
      Rectangle r = new Rectangle(p, width, height);
      
      System.out.print("Entrez l'angle d'inclinaison pour SlantedRectangle (en radians): ");
      double angle = scanner.nextDouble();
      Rectangle t = new SlantedRectangle(p, width, height, angle);
      SlantedRectangle s = new SlantedRectangle(p, width, height, angle);
      
      System.out.println("\nObjets créés:");
      System.out.println("Point p: " + p);
      System.out.println("Rectangle r: " + r);
      System.out.println("Rectangle t (référence Rectangle vers SlantedRectangle): " + t);
      System.out.println("SlantedRectangle s: " + s);
      
      System.out.println("\nTest des méthodes:");
      System.out.println("1. r.surface(): " + r.surface());
      System.out.println("2. r.contains(p): " + r.contains(p));
      System.out.println("3. t.surface(): " + t.surface());
      System.out.println("4. t.contains(p): " + t.contains(p));
      System.out.println("5. s.surface(): " + s.surface());
      System.out.println("6. s.contains(p): " + s.contains(p));
      
      System.out.print("\nEntrez un angle de rotation à appliquer à s (en radians): ");
      double rotation = scanner.nextDouble();
      s.rotate(rotation);
      System.out.println("Après rotation, s: " + s);
      
      System.out.println("\nAppuyez sur Entrée pour continuer...");
      scanner.nextLine(); scanner.nextLine();
      
      // Exercice 5
      System.out.println("\n=== Exercice 5: Dessin avec rectangles inclinés ===");
      System.out.println("La classe Dessin peut contenir des rectangles inclinés car SlantedRectangle");
      System.out.println("hérite de Rectangle. Les méthodes surface et translate fonctionnent toujours");
      System.out.println("correctement. La méthode contains fonctionne mais ne tient pas compte de");
      System.out.println("l'angle. La méthode hull fonctionne mais ne considère que la boîte englobante");
      System.out.println("non inclinée des rectangles inclinés.");
      
      System.out.println("\nAppuyez sur Entrée pour continuer...");
      scanner.nextLine();
      
      // Exercices 6-7
      System.out.println("\n=== Exercices 6-7: toString et equals ===");
      System.out.println("Comparaison des rectangles créés précédemment:");
      
      System.out.println("r.equals(t): " + r.equals(t));
      System.out.println("t.equals(s): " + t.equals(s));
      System.out.println("s.equals(new SlantedRectangle(p, width, height, angle)): " + 
                        s.equals(new SlantedRectangle(p, width, height, angle)));
      
      System.out.println("\nAffichage avec toString():");
      System.out.println("r: " + r);
      System.out.println("t: " + t);
      System.out.println("s: " + s);
      
      System.out.println("\nAppuyez sur Entrée pour continuer...");
      scanner.nextLine();
      
      // Exercices 8-10
      System.out.println("\n=== Exercices 8-10: Méthodes f ===");
      System.out.println("Création d'objets A et B...");
      
      A a = new A();
      A ab = new B();
      B b = new B();
      
      System.out.println("\nRésultats des appels:");
      System.out.println("1. a.f(a):");
      a.f(a);
      System.out.println("2. a.f(ab):");
      a.f(ab);
      System.out.println("3. a.f(b):");
      a.f(b);
      System.out.println("4. ab.f(a):");
      ab.f(a);
      System.out.println("5. ab.f(ab):");
      ab.f(ab);
      System.out.println("6. ab.f(b):");
      ab.f(b);
      System.out.println("7. b.f(a):");
      b.f(a);
      System.out.println("8. b.f(ab):");
      b.f(ab);
      System.out.println("9. b.f(b):");
      b.f(b);
      
      System.out.println("\nAppuyez sur Entrée pour continuer...");
      scanner.nextLine();

              // Exercice 11
              System.out.println("\n=== Exercice 11: instanceof ===");
              System.out.println("Tests instanceof avec les objets A et B:");
              
              System.out.println("a instanceof A: " + (a instanceof A));
              System.out.println("ab instanceof A: " + (ab instanceof A));
              System.out.println("b instanceof A: " + (b instanceof A));
              System.out.println("a instanceof B: " + (a instanceof B));
              System.out.println("ab instanceof B: " + (ab instanceof B));
              System.out.println("b instanceof B: " + (b instanceof B));
              
              System.out.println("\nAppuyez sur Entrée pour continuer...");
              scanner.nextLine();
              
              // Exercice 12
              System.out.println("\n=== Exercice 12: contains ===");
              System.out.println("Test de contains avec différents rectangles:");
              
              System.out.print("Entrez les dimensions d'un nouveau rectangle (largeur hauteur): ");
              double width2 = scanner.nextDouble();
              double height2 = scanner.nextDouble();
              Rectangle r2 = new Rectangle(p, width2, height2);
              
              System.out.print("Entrez un angle pour un nouveau SlantedRectangle (en radians): ");
              double angle2 = scanner.nextDouble();
              SlantedRectangle s2 = new SlantedRectangle(p, width2, height2, angle2);
              
              System.out.println("\nTests contains:");
              System.out.println("r.contains(r2): " + r.contains(r2));
              System.out.println("r.contains(s): " + r.contains(s));
              System.out.println("s.contains(r): " + s.contains(r));
              System.out.println("s.contains(s2): " + s.contains(s2));
              
              System.out.println("\nAppuyez sur Entrée pour continuer...");
              scanner.nextLine(); scanner.nextLine();
              
              // Exercice 13
              System.out.println("\n=== Exercice 13: ch et getCh ===");
              System.out.println("Création d'objets C et D...");
              
              C c = new C();
              C cd = new D();
              D d = new D();
              
              System.out.println("\nRésultats:");
              System.out.println("c.ch: " + c.ch);
              System.out.println("c.getCh(): " + c.getCh());
              System.out.println("cd.ch: " + cd.ch);
              System.out.println("cd.getCh(): " + cd.getCh());
              System.out.println("d.ch: " + d.ch);
              System.out.println("d.getCh(): " + d.getCh());
              
              System.out.println("\n=== Fin du programme ===");
              scanner.close();
          }
      }