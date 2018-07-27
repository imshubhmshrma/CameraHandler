# CameraHandler
Here I am creating a class CameraHandler of type NSObject. 
In this I am using UIImagePickerControllerDelegate and UINavigationControllerDelegate for image picking from Camera and Photo Library .
I am also making an action sheet to choose from the both options. 
It is very simple to use and manage . 

 
 
//
//  CameraButton.swift
//  
//
//  Created by Shubham on 11/04/18.
//  Copyright © 2018 Shubham. All rights reserved.
//


import Foundation
import UIKit


class CameraHandler: NSObject{
    static let shared = CameraHandler()
    
    fileprivate var currentVC: UIViewController!
    
    //MARK: Internal Properties
    var imagePickedBlock: ((UIImage) -> Void)?
    
    func camera()
    {
        if UIImagePickerController.isSourceTypeAvailable(.camera){
            let myPickerController = UIImagePickerController()
            myPickerController.delegate = self;
            myPickerController.sourceType = .camera
            myPickerController.allowsEditing = true
            currentVC.present(myPickerController, animated: true, completion: nil)
        }
        
    }
    
    func photoLibrary()
    {
        
        if UIImagePickerController.isSourceTypeAvailable(.photoLibrary){
            let myPickerController = UIImagePickerController()
            myPickerController.delegate = self;
            myPickerController.sourceType = .photoLibrary
            myPickerController.allowsEditing = true
            currentVC.present(myPickerController, animated: true, completion: nil)
        }
        
    }
    
    func showActionSheet(vc: UIViewController) {
        currentVC = vc
        let actionSheet = UIAlertController(title: "Upload", message: "Image from", preferredStyle: .alert)
        
        actionSheet.addAction(UIAlertAction(title: "Camera", style: .default, handler: { (alert:UIAlertAction!) -> Void in
            self.camera()
        }))
        
        actionSheet.addAction(UIAlertAction(title: "Gallery", style: .default, handler: { (alert:UIAlertAction!) -> Void in
            self.photoLibrary()
        }))
        
        actionSheet.addAction(UIAlertAction(title: "Cancel", style: .cancel, handler: nil))
        
        vc.present(actionSheet, animated: true, completion: nil)
    }
    
}


extension CameraHandler: UIImagePickerControllerDelegate, UINavigationControllerDelegate{
    func imagePickerControllerDidCancel(_ picker: UIImagePickerController) {
        currentVC.dismiss(animated: true, completion: nil)
    }
    
    func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {
        if let image = info[UIImagePickerControllerOriginalImage] as? UIImage {
            self.imagePickedBlock?(image)
            currentVC.dismiss(animated: true, completion: nil)
        }
    }
}
/* how to use this on button
 @IBAction func actionProfilePic(_ sender: UIButton) {
 print(" 🎦🎬🎬 Action Profile Tapped 🎦🎬🎬")
 CameraHandler.shared.showActionSheet(vc: self)
 CameraHandler.shared.imagePickedBlock = { (image) in
 print("",image)
 self.profileImageView.image = image
  }
}
 */ 
