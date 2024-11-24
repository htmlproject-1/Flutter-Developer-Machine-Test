# Flutter-Developer-Machine-Test
class SplashScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        children: [
          Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Image.asset('assets/dealsdray_logo.png', height: 100), // Replace with your logo
                SizedBox(height: 20),
                Text('DealsDray', style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
              ],
            ),
          ),
          Positioned.fill(
            child: Opacity(
              opacity: 0.1,
              child: Image.asset('assets/background_pattern.png', fit: BoxFit.cover), // Decorative background
            ),
          ),
        ],
      ),
    );
  }
}
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: TextField(
          decoration: InputDecoration(
            hintText: 'Search here',
            prefixIcon: Icon(Icons.search),
            border: OutlineInputBorder(borderRadius: BorderRadius.circular(8)),
          ),
        ),
        actions: [
          IconButton(icon: Icon(Icons.notifications), onPressed: () {}),
        ],
      ),
      body: SingleChildScrollView(
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Banner Section
            Container(
              color: Colors.blue[100],
              padding: EdgeInsets.all(16),
…
class ProductList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SizedBox(
      height: 200,
      child: ListView(
        scrollDirection: Axis.horizontal,
        children: [
          ProductCard(
            name: 'Nokia 8.1',
            price: '₹15,999',
            discount: '32% Off',
            imagePath: 'assets/nokia_8_1.png',
          ),
          ProductCard(
            name: 'Redmi Note 7S',
            price: '₹9,999',
            discount: '14% Off',
            imagePath: 'assets/redmi_note_7s.png',
          ),
        ],
      ),
    );
  }
}

class ProductCard extends StatelessWidget {
  final String name;
  final String price;
  final String discount;
  final String imagePath;

  ProductCard(…
dependencies:
  firebase_auth: ^4.7.2
  cloud_firestore: ^5.5.1
  provider: ^6.1.5
import 'package:flutter/material.dart';
import 'package:firebase_auth/firebase_auth.dart';

class PhoneInputScreen extends StatefulWidget {
  @override
  _PhoneInputScreenState createState() => _PhoneInputScreenState();
}

class _PhoneInputScreenState extends State<PhoneInputScreen> {
  final TextEditingController _phoneController = TextEditingController();

  void _sendOtp() async {
    String phoneNumber = _phoneController.text.trim();
    await FirebaseAuth.instance.verifyPhoneNumber(
      phoneNumber: phoneNumber,
      verificationCompleted: (PhoneAuthCredential credential) {
        // Auto-resolve OTP (rare cases)
      },
      verificationFailed: (FirebaseAuthException e) {
        ScaffoldMessenger.of(context).showSnackBar(SnackBar(content: Text(e…
import 'package:flutter/material.dart';
import 'package:firebase_auth/firebase_auth.dart';

class OtpVerificationScreen extends StatefulWidget {
  final String verificationId;

  OtpVerificationScreen({required this.verificationId});

  @override
  _OtpVerificationScreenState createState() => _OtpVerificationScreenState();
}

class _OtpVerificationScreenState extends State<OtpVerificationScreen> {
  final TextEditingController _otpController = TextEditingController();

  void _verifyOtp() async {
    String otp = _otpController.text.trim();
    try {
      PhoneAuthCredential credential = PhoneAuthProvider.credential(
        verificationId: widget.verificationId,
        smsCode: otp,
      );
      UserCredential userCredential =
          await FirebaseAu…
import 'package:flutter/material.dart';

class RegistrationScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Register')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              decoration: InputDecoration(labelText: 'Enter Email'),
            ),
            TextField(
              decoration: InputDecoration(labelText: 'Create Password'),
              obscureText: true,
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                // Handle Registration
              },
              child: Text('Register'),
            ),
          ],
        ),
      ),
    );
  }
}
void main() {
  runApp(MaterialApp(
    initialRoute: '/',
    routes: {
      '/': (context) => PhoneInputScreen(),
      '/landingPage': (context) => LandingPage(),
      '/registrationPage': (context) => RegistrationScreen(),
    },
  ));
}
