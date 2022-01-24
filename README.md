# Grocery-List-App

Say goodbye to the old-fashioned grocery list and welcome this App! One place for you and your family members to manage your grocery list .. YAY TEAMWORK!

And adding my own :sparkles: Touch :sparkles: to it ... you'll be drowned in a sea of confetti with almost every click ... cuz why not? :)

*Note : Enjoy the light and dark modes too !*
## App Preview

https://user-images.githubusercontent.com/85634099/150640219-5808d34d-3f49-4331-9710-146cf8f17a02.mp4

## Accounts
### 1) Log In
To start you need to login into your account in [firebase](https://firebase.google.com/docs/auth/ios/start) using email & password , you can also login into your [google](https://developers.google.com/identity/sign-in/ios/start-integrating) or [facebook](https://developers.facebook.com/docs/facebook-login/ios/) account.

https://user-images.githubusercontent.com/85634099/150684142-77384779-05a7-49ab-8ea3-48d36e9faebe.mp4

### 2) Register
If haven't registered yet, no worries, just navigate to the registration page by clicking on (Register Now) at the bottom of the screen and enter your email and password .. and voila! you just created your account :)


https://user-images.githubusercontent.com/85634099/150794729-89ea2d25-4854-4b2e-94cf-27c54cf262b8.mp4


### 3) Online Accounts & Sign Out
Once you are logged in, you will notice a number at the top-left corner of the screen indicating the number of users logged in the app.

By clicking on the number it will navigate you into a list showing all the online accounts, and a sign out button at the top-right corner which will sign you out to be redirected back to the login page

https://user-images.githubusercontent.com/85634099/150807896-3347492e-c8dc-4570-a511-1f5726e047a1.mp4
 
## Grocery Items

### 1) Add Item
Click on the plus button on the top-right corner of the screen for a dialog to pop up where you can enter your new item to be added then celebrated with loads of confetti made of the item name ;)


https://user-images.githubusercontent.com/85634099/150855538-0b5b8ff5-88fd-41d2-b96e-d5c269758747.mp4


### 2) Edit Item
In case you want to edit your item just click on the pen icon next to the item name then edit and save then celebrate your edited item once again with a rain of colorful confetti :)

*Note: you can't edit any items added by other users, you can edit the items added by you only*


https://user-images.githubusercontent.com/85634099/150855679-de9ff6bb-921a-453d-a77a-08dcf1caea6f.mp4


### 3) Item Status
Each item on that list has a status as complete/incomplete which is indicated by the check box on the right side of the item, to change the status of any item just click on the checkbox and a dialog will appear to choose the status from, if the item is marked as completed it will be crossed with a red mark and it will show a checkmark to indicate that it is completed otherwise (if it is incomplete) the checkbox will appear empty with no checkmark.

*Note: you can change the status of the items added by other users too*


https://user-images.githubusercontent.com/85634099/150855988-e0969880-55c2-4227-a763-372e3bf37238.mp4


### 4) Delete Item
If you don't need that item anymore, a swipe to the left and we will say bye-bye to that item with a rain of red confetti :)

*Note: you can't delete any items added by other users, you can delete the items added by you only*


https://user-images.githubusercontent.com/85634099/150854975-ea280830-1d97-4e1d-a490-70eba36d99f0.mp4



## Progress Bar
To Keep track of your progress, the items' status is presented by a progress bar indicating how many items are marked as completed in your list. As long as they are not all completed, the progress bar will be displayed with an orange color and once you mark all the items as completed it will change its color into green .. AND ... YOU GUESSED IT !! IT'S CONFETTI TIME !!

https://user-images.githubusercontent.com/85634099/150856154-27ca4b0d-05bb-4f56-9ad5-0837b4ae6f53.mp4



## Confetti 
As I always say "You can't call it an App if it doesn't drown you in a sea of Confetti", so we got to celebrate with each click with loads of confetti in all shapes, sizes, and colors, and let's see how it's done...

## Regualr Confetti 

I used regular confetti shape for celebrating the completion of all grocery items , you can find it in [here](https://github.com/sudeepag/SAConfettiView), you can specify the type and shape of the confetti and more as follows :
```
        let confettiView = SwiftConfettiView(frame: (self.view.bounds))// for the confetti to cover the full screen
        self.view.addSubview(confettiView)// add the confetti view to the screen
        confettiView.type = .confetti // set the type to normal confetti
        confettiView.colors = [UIColor.red,UIColor.green,UIColor.yellow,UIColor.blue] // set the colors of the confetti
        confettiView.intensity = 1.0
        confettiView.layer.speed = 1.5
        confettiView.startConfetti() 
```


https://user-images.githubusercontent.com/85634099/150858752-cd494eae-7e1f-4ac2-9104-7d02c94fa05a.mp4


## Text Based Confetti
After an item is (added/edited/deleted) a sea of custom confetti appears with the name of the item that was just modified or deleted and it follows these steps in order :

### 1) Text To Image
Get the item name as a text and pass it through this extension to convert it from text to an image.

```
extension UIImage {// used to convert Text into Images
    class func imageWithLabel(label: UILabel) -> UIImage {
        UIGraphicsBeginImageContextWithOptions(label.bounds.size, false, 0.0)
        label.layer.render(in: UIGraphicsGetCurrentContext()!)
        let img = UIGraphicsGetImageFromCurrentImageContext()
        UIGraphicsEndImageContext()
        return img!
   }
}
```

### 2) Pick Random Color
Having the same color is boring, however, the colors are based upon a CGFloat value, so I used the following extension which will return a random CGFloat value that I will use to generate a random color in step 3.
```
extension CGFloat {// returns a random value to be used to retrive a random UICOLOR
    static func random() -> CGFloat {
        return CGFloat(arc4random()) / CGFloat(UInt32.max)
    }
}
```
### 3) Get Color Palette
Now use the random function from the extension in step 2 to return 3 random CGFloat values representing red, green, and blue values resulting in a new UIColor!


and as confetti are made of multiple colors, we want the colors to look nice together so i added 2 more functions called darker and lighter which basically return a dark and a light version of the original color that we passed through the function (ex: we pass the color blue and we will get dark blue and light blue)
```
extension UIColor {// uses the CGFloat random function to get the red , green and blue values and generate a random color
    static func random() -> UIColor {
        return UIColor(
           red:   .random(),
           green: .random(),
           blue:  .random(),
           alpha: 1.0
        )
    }

    func lighter(by percentage: CGFloat = 30.0) -> UIColor? {// to return a lighter version of the provided UICOLOR
        return self.adjust(by: abs(percentage) )
    }

    func darker(by percentage: CGFloat = 30.0) -> UIColor? {// to return a darker version of the provided UICOLOR
        return self.adjust(by: -1 * abs(percentage) )
    }

    func adjust(by percentage: CGFloat = 30.0) -> UIColor? {// change the color depending on the passed percentage (lighter\darker)
        var red: CGFloat = 0, green: CGFloat = 0, blue: CGFloat = 0, alpha: CGFloat = 0
        if self.getRed(&red, green: &green, blue: &blue, alpha: &alpha) {
            return UIColor(red: min(red + percentage/100, 1.0),
                           green: min(green + percentage/100, 1.0),
                           blue: min(blue + percentage/100, 1.0),
                           alpha: alpha)
        } else {
            return nil
        }
    }
}

```
*Note: when we delete an item the Text Based Confetti will work the same except that it will use red color only to indicate that the item has been deleted*

### 4) Put It All Togather
After converting the text into an image and generating our random color and it's pallete now we will use them in the following confetti function in which we pass the text image from step 1 as an argument and use the colors we created in step 2 & 3 which are stored in a list named "myColorsList"
```
func Confetti(customImage : UIImage){
       
         let confettiView = SwiftConfettiView(frame: (self.view.bounds))// for the confetti to cover the full screen
         self.view.addSubview(confettiView)// add confetti to the screen
         confettiView.type = .image(customImage) // set the confetti type to image to use the text image we created eearlier
         confettiView.colors = myColorsList // use the colors we geberated earlier whcih are stored within this list
         confettiView.intensity = 0.5
         confettiView.layer.speed = 1
         confettiView.startConfetti()
         
         }
```

https://user-images.githubusercontent.com/85634099/150862743-7dfeed90-8ebd-4084-892a-3cf7d9b20f9a.mp4




