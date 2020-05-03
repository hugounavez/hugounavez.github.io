---
layout: post
title:  "Model View ViewModel SwiftUI template"
#date:   2019-03-23 21:03:36 +0530
categories: SwiftUI iOS
---

Back to 2016 when I started to work in Mobile Development, the default architectural pattern was the model view Controller (or MVP in android). Basically with this pattern there is no a significant separation between the elements: in the model class stores the data, the view just deals with views and rest goes to the controller. In consequence, developers had to deal with massive controllers with probably thousands lines of code because all business logic had no other place to live.
 
## MVVM to the rescue
 
Then, the Model View ViewModel came to our lives and make everything more manageable so now we can easily split the code and distribute responsibilities between the components. 

In this architectural pattern the model keeps the same as in the previous pattern, the view keeps the code related to rendering the UI elements, but the viewModel has to work kind of like a bridge between the view and the model. Basically, this new component has to deal with the data, networking,  and also the information processes (such as calculations, etc) and communicate the changes with the view (all theses actions were placed in the controller before).
 
One important point is how we can set the elements in a way that they can talk to each other with no issues. This is possible more than ever with the observable property but we are going to start the example with the model, because is the easiest part.
 
The model for this example is going to be a Person object which only has one attribute. This object will represent a the single data structure that stores all information needed for the view.
 
#### Model
```swift
struct Person{
    var name: String = "Hugo"
}
```

As I mentioned before, the view model is going to handle the data, http requests, data processing etc, but in this simple example, we are going to just simply instantiate the model object: 
 
#### ModelView
```swift
class ViewModel: ObservableObject{
    // Model instantiation
    @Published var model : Person = Person() // Here the viewModel has access to the model. 
    
    // This an example function to simulate a http request.
    func getDataFromRestAPI(){
        // Updating name attribute
        self.model.name = "new data"
    }
}
```
 
Just to make emphasis, this particular line declares the model inside the viewModel as a Published variable, so this variable will notify any entity that is watching her. 
```swift
    @Published var model : Person = Person() // Here the viewModel has access to the model. 
```

#### View

In the content view we instantiate the viewModel as an observedObject, so any change is going to be perceived. 

```swift
struct ContentView: View {
    // The viewModel is instantiated
    @ObservedObject var viewModel  = ViewModel()
    var body: some View {
        VStack {
            Spacer() // Make space
            TextField("Placeholder", text: $viewModel.model.name)
            Spacer() // Make space
            Text(viewModel.model.name)
            Spacer() // Make space
        }
        
    }
}
```
 
Here the text from the text field is attached to the attribute name of the model object in the view model. In other words:
 
The controller is seeing the viewModel as an ObservedObject so there is communication between the view and viewModel: 

```swift
TextField("Placeholder", text: $viewModel.model.name)
```

The same for this line, in which the text label is binded to view.model.name property:

```swift
Text(viewModel.model.name)
```

When  you run the app, you must get this screen:
<p style="text-align: center">
    <img src="/assets/images/1.png"  alt="drawing" width="300"/>
</p>

If you change the text by typing in the text field, the label will also change in the meantime.

<p style="text-align: center">
    <img src="/assets/images/2.png"  alt="drawing" width="300"/>
</p>


