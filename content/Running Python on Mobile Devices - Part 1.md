---
title: Running Python on Mobile Devices - Tensorflow & ML
draft: false
tags:
  - technical
date: 2024-06-24
---
 I initially wrote this reflection as one very long piece, but there is a natural break in the two segments, with different skills developed. Therefore, I have split them into two reflections. 
 
 One of the customer pilot's largest technical challenges was providing users with hydration, fatigue and heat stress scores while offline. This is difficult as it requires running machine learning (ML) models frequently on devices with restricted battery life and processing power, compared to hosting the models on an online server and returning the results to the user over the internet. 

The initial version of the ML models was created using a popular Python package, "sci-kit learn," which runs well on computers and servers but can't be natively run on mobile devices. To resolve this, I investigated what frameworks were popular to run ML models on devices. I learnt that Apple offers CoreML for iOS devices and Google offers TensorFlow Lite for Android. As Google also created the framework Flutter, which the mobile application was already written in, TensorFlow Lite was available there, too. Therefore, we selected TensorFlow Lite as the most logical option for working on the devices. This would allow us to use the models for the pilot and only need to create CoreML models once the application has been migrated to Kotlin Multi-Platform.

After a week of development from our Data Science team, I was supplied with the models to run on the device. I successfully ran the models on a sample input and provided an example of the basic code with annotations to run a TensorFlow model in Flutter.


```dart title="Tensorflow Lite Example"
import 'package:tflite_flutter/tflite_flutter.dart' as tfl;

Future<List<String>> tensorFlowExample() async {
	//Import model files from the device's install folder
	final heatCateogry = await tfl.Interpreter.fromAsset('model_clf.tflite');
	final heatStress = await tfl.Interpreter.fromAsset('model_reg1.tflite');
	final heatChange = await tfl.Interpreter.fromAsset('model_reg2.tflite');
	
	//Create the models from the files
	final isolateCategory = await tfl.IsolateInterpreter.create(address: heatCateogry.address);
	final isolateStress = await tfl.IsolateInterpreter.create(address: heatStress.address);
	final isolateChange = await tfl.IsolateInterpreter.create(address: heatChange.address);
	//An example matrix input, the values can not be labelled due to NDA
	var input = [[33.3, 39, 0, 58.45, 36.76, 1031.473684, 105.8884062, 58.16920094, 58.81066145, 6.2817225, 49.42339374, 72.02881152, 82.33468285, 21, 55.26315789]];
	
	//Create the matrix to store the output of the model of each model
	var outputCategory = List.filled(1*1, 0).reshape([1,1]);
	var outputStress = List.filled(1*1, 0).reshape([1,1]);
	var outputChange = List.filled(1*1, 0).reshape([1,1]);
	
	//Run the models and store the final result in an array for displaying to the user
	List<String> result = [];
	await isolateCategory.run(input, outputCategory);
	result.add(outputCategory[0][0].toString());
	await isolateStress.run(input, outputStress);
	result.add(outputStress[0][0].toString());
	await isolateChange.run(input, outputChange);
	result.add(outputChange[0][0].toString());
	return result;
}
``` 
<p style="text-align: center; font-style: italic;">
Artefact: Adapted code from our repo to run TensorFlow models in Dart</p>  

However, I didn't realise then that success was further away than it appeared. Although we could easily run the models on the device, a crucial step in the ML pipeline is to pre-process the data to transform it from raw values into a structure that can be input into the model. The team had written this code in Python and used many Python-specific packages; as a solo developer, it was impossible to translate this pre-processing step before the deadline. 

My takeaway from this experience is that my idea of planning the project did not dive deep enough into the implementation details. I had a surface-level understanding of how the ML pipeline works and the ability to run ML models on smartphones. However, the issues I discovered during implementation should have been discovered during research of the issue at the planning stage, which I skipped, believing that my knowledge was sufficient. Moving forward, I will dedicate more time to the planning stage, not only due to this failure but also because I believe the better scoped, researched and documented a project and each individual step within is, the easier it is to implement the feature.

The final process of running Python on devices is covered in [[Running Python on Mobile Devices - Part 2]].