# Blocks save to execute later

## Example callbacks

```
class SaveListener
   def on_save(doc)
     puts "hey i'm saving!"
   end
end

class Document
  attr_accessor :save_listener

  def save
    save_listener.on_save(self) if save_listener
  end
end

# execute

doc = Document.new
doc.save_listener = SaveListener.new

doc.save

```
