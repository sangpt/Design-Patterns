# 1. Factory Design Pattern

- Class diagram
![image](https://i.imgur.com/XBtwwlb.jpg)

- Source code

```
class Shape
  def draw
    raise 'must implement draw() method in subclass'
  end
end

class Rectangle < Shape
  def draw
    puts 'Inside Rectangle::draw() method.'
  end
end

class Square < Shape
  def draw
    puts 'Inside Square::draw() method.'
  end
end

class Circle < Shape
  def draw
    puts 'Inside Circle::draw() method.'
  end
end

class ShapeFactory
  def get_shape(type)
    case type
    when 'Circle'    then Circle.new
    when 'Rectangle' then Rectangle.new
    when 'Square'    then Square.new
    end
  end
end

shape_factory = ShapeFactory.new

circle = shape_factory.get_shape('Circle')
circle.draw

rectangle = shape_factory.get_shape('Rectangle')
rectangle.draw

square = shape_factory.get_shape('Square')
square.draw
```

- Chi can su dung doi tuong cua lop ShapeFactory de tao cac Shape ma khong can chi ro cu the Shape nao se duoc tao
