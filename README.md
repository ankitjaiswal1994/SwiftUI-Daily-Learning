# SwiftUI-Daily-Learning

# First Day 

### What benefits I found

1. Less code and less configuration to start.
2. PreviewProviders can easily help to run a small part of the apps without actually compiling a complete application.
3. Complete UI is visible on the other side of the window.
4. For the component requiring props/parameter, we can mock the data in PreviewProvider and see the result. This makes easy for other developers to reuse and the component and see the working of a single component.
5. Components can be easily isolated and tested.
6. Hot reloading benefits : In other technology like react native you still have to run the app once and while coding if some javascript error occurs you need to relaod the application but here in SwiftUI while typing you will see the changes and even some syntacx error u made it just stops rendering and if you correct it, it will work in the same way.
7. You can add as many devices for preview providers. So easy to see component on different devices.
8. Any you change in the SwiftUI components from the SwiftUI inspector it gets coded along with change unlike storyboards and xibs which creates alot of confusion. Some changes were from the code and some from the storyboard/xib UI. This will help in code review and also for theming.
9. Code like a html where padding, alignment, margin works. 

Maybe some points does not makes sense to you but do not worry it will after sometime you can jump back again and see.

I will keep adding if I found more.


### What I learned on Day 1

1. No appdelegates or scenedelegates. Strange for me, so I decided how to change the navigation bar appearance.
Below is the initial point of entry.

```
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
```

So to apply any changes you cannot just write below `ContentView()` as it expects to return a view. Instead you can use init give any configuration.

```
init() {
        UINavigationBar.appearance().backgroundColor = .yellow
}
```


2. **Components** If you want to return multiple views inside ContentView. You cannot just simply write two views. You need to bind it in a group, stack or list. Now is point you can hit and try and use components like Text, Image and try to giving padding, alignments etc. Use `Spacer()` it is just like `space-between` in css. One more thing I also used `HStack` and `VStack` here give it a try its like row and column based design.

3. **List** The main component within any application is the List. Previously we were using `UITableView` which scatters our code like cell is somewhere else, data is somewhere else, few different delegates and datasources. Inshort we need to write alot of code for this. But swiftUI provides `List` which is very easy to use.
Give it a try -> https://www.hackingwithswift.com/quick-start/swiftui/how-to-create-a-list-of-dynamic-items

Note: List expects unique id, in the example you will see the Model is conforming the protocol `Identifiable`, This protocol has only one requirement, which is that conforming types must have a property called id that can identify them uniquely. I think this is the best practice we should always conform the protocol `Identifiable`.

What happen if your model doesnt conform `Identifiable` protocol. No worries, you can define the id while iterating `List` like
```
ForEach(expenses.items, id: \.id) { item in
    Text(item.name)
}
```
But if your items already have id then your code will become
```
ForEach(expenses.items) { item in
    Text(item.name)
}
```

Second one will be the best practice.

3. **Navigation setup** If you were using UIKit this will blow your mind. You do not need to define any storyboard ids or do not need to load any xibs for navigation. Just wrap your view with `Navigation View` and see the content preview, navigation will be shown. Now you can give `.navigationBarTitle` or color upto you use an many properties you can. 

`Navigation` now how to navigate to another screen. No hustle just wrap your view with `NavigationLink` like

```
        NavigationView {
            List(hikes) { hike in
                NavigationLink(
                    destination: HikeDetail(hike: hike),
                    label: {
                        HikeCell(hike: hike)
                    })
            }
            .navigationBarTitle("Hiking List")
        }
```
This was from my hiking project example. 

Even you can pass `Text` in the destination like

```
destination: Text("Detail Page"),
```

`Tip`: Since I used to work on React-Native. I follow component based approach like break your screens into small-small components and create different component and configure it via props/paramter. So that it can be reusable by anyone and shared accross the project and with the props/parameter anyone can configure it from outside and reuse it in whatever way they want. In `SwiftUI` we can easily follow this and even test this via PreviewProvider.

After writing code `SwiftUI` gives you an option to extract your component within a separate subview. Just select your component press `command + click`. You see the option to `Extract Subview` like below:

<img width="430" alt="Screenshot 2021-05-20 at 1 45 19 PM" src="https://user-images.githubusercontent.com/20721521/118944130-e935eb00-b971-11eb-9cc5-eefd321cc913.png">

Now over to you try it. Even try `Show SwiftUI Inspector` on `Text` and try to change the UI you will it get refelected on your code on the left panel.

