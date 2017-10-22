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


# 2. Template method Design Pattern

- Class diagram
![image](https://i.imgur.com/CxWsbHc.png)

- Source code

```
class ReportTemplate
  def initialize
    @title = 'Monthly Report'
    @text =  ['Sample text 1', 'Sample text 2', 'Sample text 3']
  end

  def output_report
    output_start
    output_head
    output_body_start
    @text.each { |line| output_line(line) }
    output_body_end
    output_end
  end

  def output_start
  end

  def output_head
    output_line(@title)
  end

  def output_body_start
  end

  def output_line(_line)
    raise 'Called abstract method: output_line'
  end

  def output_body_end
  end

  def output_end
  end
end

class PlainTextReport < ReportTemplate
  def output_start
  end

  def output_head
    puts "**** #{@title} ****"
    puts
  end

  def output_body_start
  end

  def output_line(line)
    puts line
  end

  def output_body_end
  end

  def output_end
  end
end

class HTMLReport < ReportTemplate
  def output_start
    puts '<html>'
  end

  def output_head
    puts '  <head>'
    puts "    <title>#{@title}</title>"
    puts '  </head>'
  end

  def output_body_start
    puts '<body>'
  end

  def output_line(line)
    puts "  <p>#{line}</p>"
  end

  def output_body_end
    puts '</body>'
  end

  def output_end
    puts '</html>'
  end
end


report = HTMLReport.new
report.output_report

report = PlainTextReport.new
report.output_report
```
