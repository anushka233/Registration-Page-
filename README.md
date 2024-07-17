# Registration-Page-

import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'package:firebase_auth/firebase_auth.dart';
import 'package:fluttertoast/fluttertoast.dart';

class RegistrationScreen extends StatefulWidget {
  const RegistrationScreen({super.key});

  @override
  State<RegistrationScreen> createState() => _RegistrationScreenState();
}

class _RegistrationScreenState extends State<RegistrationScreen> {
  String emailAddress="",password="",name="";
  bool showPass= true;
  bool validateUser = false;
  final authInstance = FirebaseAuth.instance;
  @override
  Widget build(BuildContext context) {
    return  Scaffold(
      backgroundColor: const Color.fromARGB(255, 215, 206, 206),
      body: Column(children: [
        const Text("Register Here",style: TextStyle(color: Colors.white,fontWeight: FontWeight.bold,fontSize: 40)),
        const SizedBox
        (
          height:20
          ),
          const Text("Please the details here as per requirement mentioned*",style: TextStyle(color: Colors.white,fontWeight: FontWeight.bold,fontSize: 20)),
          const SizedBox(
            height: 40,
          ),
          validateUser== true? const Text("Please check all the fields"):const Text(""),
          Padding(
            padding: const EdgeInsets.only(left: 200,right: 200),
            child: TextField(
              onChanged: (email){
                emailAddress = email;
              },
              keyboardType: TextInputType.emailAddress,
              decoration: InputDecoration(
                filled: true,
                fillColor: Colors.white,
                hintText: "Please enter the email address",
                border: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(10)
                ),
              ),

            ),
          ),
          const SizedBox(
            height: 40,
          ),
         Padding(
            padding: const EdgeInsets.only(left: 200,right: 200),
            child: TextField(
              onChanged: (name){
                name = name;
              },
              keyboardType: TextInputType.name,
              decoration: InputDecoration(
                filled: true,
                fillColor: Colors.white,
                hintText: "Please enter the Name",
                border: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(10)
                ),
              ),
 
            ),
          ),
          const SizedBox(
            height: 40,
          ),
          Padding(
            padding: const EdgeInsets.only(left: 200,right: 200),
            child: TextField(
              onChanged: (pass){
               password = pass;
              },
              obscureText: showPass,
              decoration: InputDecoration(
                filled: true,
                fillColor: Colors.white,
                hintText: "Please enter your Password",
                border: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(10)
                ),
                suffixIcon: GestureDetector(
                  onTap: (){
                    setState((){
                      showPass = !showPass;
                    });
                  },
                  child: showPass? const Icon(Icons.visibility_off): const Icon(Icons.visibility)),
              ),

            ),
          ),
          const SizedBox(
            height: 40
          ),
          RawMaterialButton(
            onPressed: ()async{
              if(emailAddress != "" && password != ""){
                setState(() {
                  validateUser = false;
                });
                try{
              await authInstance.createUserWithEmailAndPassword(email: emailAddress, password: password);
                }
                catch(error){
                  print("Error is there $error");
                  Fluttertoast.showToast(msg: error.toString());
                }
              }
              else{
                setState(() {
                  validateUser = true;
                });
              }
            },
            elevation: 3,
            fillColor: Colors.white,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(23)
              ),
              child: const Padding(
                padding: EdgeInsets.only(left: 100,right: 100,top: 10,bottom: 1),
                child: Text("REGISTER",style: TextStyle(fontSize: 20,color: Colors.black), 
                ),
              ),
              )

      ],)
    );
  }
}
