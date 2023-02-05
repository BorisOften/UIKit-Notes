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

## ScrollView with dynamic height with Example

Rather than using a view with a fixed height, we could use a stack view inside the scroll view. 
This will make the srcollview dynamic and then we can just add other views in the stack view

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

we can adapt the scrollview for our own needs: add TextFields, UIImageView, Segmented Controls or whatever we need to build our user interface.

## Links
- https://www.youtube.com/watch?v=JEtMmiRX_c8
- https://medium.com/swift-productions/create-a-uiscrollview-programmatically-xcode-12-swift-5-3-f799b8280e30
- https://www.youtube.com/watch?v=-yjknIzf5KE
