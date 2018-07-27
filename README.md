# CameraHandler
Here I am creating a class CameraHandler of type NSObject. 
In this I am using UIImagePickerControllerDelegate and UINavigationControllerDelegate for image picking from Camera and Photo Library .
I am also making an action sheet to choose from the both options. 
It is very simple to use and manage . 
First create a button(on click you want the camera and photo library access) and create a action of that button 
and add  

@IBAction func actionImageButtonTapped(_ sender: UIButton) {
 print(" 🎦🎬🎬 Button Tapped 🎦🎬🎬") 
 CameraHandler.shared.showActionSheet(vc: self)
 CameraHandler.shared.imagePickedBlock = { (image) in
 print("the image that is picked",image)
 self.imageView.image = image // here imageView in a imageView on which you want to show the image that is being picked up 
  } 
 }
 
 
 
