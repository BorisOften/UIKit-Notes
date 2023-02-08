# ScrollView
** ( add gif)

There are two types of scroll view, fixed and dynamic. 
For the fixed scrollview, we can embed a view in the scrollview,
while we can use a stackview to make the scrollview dynamic

## ScrollView with fixed height with Example

Here we place a view with a fixed height inside the scrollview

```swift 
import UIKit

class ViewController: UIViewController {

    let scrollView = UIScrollView()
    let newContentView = UIView()
    
    let image1 = UIImageView(image: UIImage(named: "bunny"))
    let image2 = UIImageView(image: UIImage(named: "dog"))
    
    override func viewDidLoad() {
        super.viewDidLoad()

        setup()
    }

    func setup()  {
        view.addSubview(scrollView)
        
        scrollView.addSubview(newContentView)
        
        newContentView.addSubview(image1)
        newContentView.addSubview(image2)

        scrollView.translatesAutoresizingMaskIntoConstraints = false
        newContentView.translatesAutoresizingMaskIntoConstraints = false
        newContentView.backgroundColor = .systemPink
        
        image1.translatesAutoresizingMaskIntoConstraints = false
        image1.contentMode = .scaleAspectFill
        
        image2.translatesAutoresizingMaskIntoConstraints = false
        image2.contentMode = .scaleAspectFill
        
        NSLayoutConstraint.activate([
            scrollView.topAnchor.constraint(equalTo: view.topAnchor),
            scrollView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
            scrollView.bottomAnchor.constraint(equalTo: view.bottomAnchor),
            scrollView.trailingAnchor.constraint(equalTo: view.trailingAnchor)
        ])

        NSLayoutConstraint.activate([
            newContentView.topAnchor.constraint(equalTo: scrollView.topAnchor),
            newContentView.leadingAnchor.constraint(equalTo: scrollView.leadingAnchor),
            newContentView.bottomAnchor.constraint(equalTo: scrollView.bottomAnchor),
            newContentView.trailingAnchor.constraint(equalTo: scrollView.trailingAnchor),
            
            // We have to add a width anchor so that while scrolling, the stack view will always
            // have the same width as the scroll view
            // If we do not set this, the stackView width may extend pass the view of the screen and we have to scroll horizontally
            newContentView.widthAnchor.constraint(equalTo: view.widthAnchor),
            // we have to give this view a height constant because it is in a scroll view
            newContentView.heightAnchor.constraint(equalToConstant: 1000)
        ])
        
        //image 1
        NSLayoutConstraint.activate([
            image1.topAnchor.constraint(equalTo: newContentView.topAnchor),
            image1.leadingAnchor.constraint(equalTo: newContentView.leadingAnchor),
            image1.trailingAnchor.constraint(equalTo: newContentView.trailingAnchor),
        ])

        //image 2
        NSLayoutConstraint.activate([
            image2.topAnchor.constraint(equalTo: image1.bottomAnchor),
            image2.leadingAnchor.constraint(equalTo: newContentView.leadingAnchor),
            image2.trailingAnchor.constraint(equalTo: newContentView.trailingAnchor),
        ])
    }
}
```
### Steps
First we created a scrollView and set the scrollView to fill the viewcontrollers' view. Then we added a view with a fixed height inside the scrollview.
This view fills out the scrollview
thats it, we can then design and add other views to the content view 

## ScrollView with dynamic height

Rather than using a view with a fixed height, we could use a stack view or a view without a fixed height. For the stackview, we just add a stackView inside the scroll view. For a normal view, we just have to make sure every constraint is connecting from contentView.TopAnchor to contentView.BottomAnchor. So, there should be a view that has it's topanchor 
This will make the scrollview dynamic and then we can just add other views in the stack view

# Example - StackView

```swift
import UIKit

class ViewController: UIViewController {

    let scrollView = UIScrollView()
    let stackView = UIStackView()

    override func viewDidLoad() {
        super.viewDidLoad()

        setup()
    }

    func setup()  {
        view.addSubview(scrollView)
        scrollView.addSubview(stackView)

        scrollView.translatesAutoresizingMaskIntoConstraints = false
        
        stackView.translatesAutoresizingMaskIntoConstraints = false
        stackView.axis = .vertical

        NSLayoutConstraint.activate([
            scrollView.topAnchor.constraint(equalTo: view.topAnchor),
            scrollView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
            scrollView.bottomAnchor.constraint(equalTo: view.bottomAnchor),
            scrollView.trailingAnchor.constraint(equalTo: view.trailingAnchor)
        ])

        NSLayoutConstraint.activate([
            stackView.topAnchor.constraint(equalTo: scrollView.topAnchor),
            stackView.leadingAnchor.constraint(equalTo: scrollView.leadingAnchor),
            stackView.bottomAnchor.constraint(equalTo: scrollView.bottomAnchor),
            stackView.trailingAnchor.constraint(equalTo: scrollView.trailingAnchor),
            
            // We have to add a width anchor so that while scrolling, the stack view will always
            // have the same width as the scroll view
            // If we do not set this, the stackView width may extend pass the view of the screen and we have to scroll horizontally 
            stackView.widthAnchor.constraint(equalTo: scrollView.widthAnchor)
        ])
    }
}

```

# Example - UIView

``` swift
import UIKit

class ViewController: UIViewController {

    let scroll = UIScrollView()
    let contentView = UIView()
    let firstLabel = UILabel()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setup()
    }

    func setup() {
        view.addSubview(scroll)
        
        scroll.addSubview(contentView)
        contentView.addSubview(firstLabel)
        
        scroll.translatesAutoresizingMaskIntoConstraints = false
        scroll.backgroundColor = .blue
        
        contentView.translatesAutoresizingMaskIntoConstraints = false
        contentView.backgroundColor = .red
        
        firstLabel.translatesAutoresizingMaskIntoConstraints = false
        firstLabel.text = "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum. Aenean imperdiet. Etiam ultricies nisi vel augue. Curabitur ullamcorper ultricies nisi. Nam eget dui."
        firstLabel.font = .systemFont(ofSize: 30, weight: .bold)
        firstLabel.numberOfLines = 0
        
        NSLayoutConstraint.activate([
            scroll.topAnchor.constraint(equalTo: view.topAnchor),
            scroll.leadingAnchor.constraint(equalTo: view.leadingAnchor),
            scroll.trailingAnchor.constraint(equalTo: view.trailingAnchor),
            scroll.bottomAnchor.constraint(equalTo: view.bottomAnchor),
        ])
        
        NSLayoutConstraint.activate([
            contentView.topAnchor.constraint(equalTo: scroll.topAnchor),
            contentView.leadingAnchor.constraint(equalTo: scroll.leadingAnchor),
            contentView.trailingAnchor.constraint(equalTo: scroll.trailingAnchor),
            contentView.bottomAnchor.constraint(equalTo: scroll.bottomAnchor),
            contentView.widthAnchor.constraint(equalTo: scroll.widthAnchor)
         ])
        
        NSLayoutConstraint.activate([
            firstLabel.topAnchor.constraint(equalTo: contentView.topAnchor, constant: 30),
            firstLabel.leadingAnchor.constraint(equalTo: contentView.leadingAnchor, constant: 10),
            firstLabel.trailingAnchor.constraint(equalTo: contentView.trailingAnchor, constant: -10),
        ])
    }
}
```
Here, we have a label in the contentView of the scrollview but because we never use the contentView's bottom anchor, the contentView does not know what height it should be and therefore it is not scrollable.
If we add the code in the NSLayoutConstraint.activate of the firstlabel as shown below, it show make contentView scrollable

```swift
firstLabel.bottomAnchor.constraint(equalTo: contentView.bottomAnchor)
```

we can adapt the scrollview for our own needs: add TextFields, UIImageView, Segmented Controls or whatever we need to build our user interface.

## Links
- https://www.youtube.com/watch?v=JEtMmiRX_c8
- https://medium.com/swift-productions/create-a-uiscrollview-programmatically-xcode-12-swift-5-3-f799b8280e30
- https://www.youtube.com/watch?v=-yjknIzf5KE
- https://stackoverflow.com/questions/37223709/using-scroll-view-with-autolayout-swift
