---
layout: post
title:      "Iteration Basics "
date:       2020-01-15 19:29:47 +0000
permalink:  iteration_basics
---


           Iteration is defined as the act or process of repeating.  Specifically in computer programming defined as a process where a set of instructions or structures are repeated in a sequence  a specified number of times or until a condition is met.  Iterators, also referred to as enumerables, are used in methods to execute a loop of code.  
	In Ruby, iterating is taking a collection of data, as an array or hash, using a iterator to operate on each member of the collection.  Then returning a new hash of the changed data. Unless using the ‘each’ enumerator, which then will always just return the original array passed in.  Using ‘map’ or ‘collect’ enumerators will give you an updated array/hash.  ‘Detect’ will give you the first piece of the array that meets the criteria set forth. ‘Select’ will give you just the pieces out of the array that match the criteria. 
 In processing an iteration between your array and your enumerable you need a . dot followed by a do command, followed by your block parameter.  A block parameter is the piece of the array you wish invoke the instructions or conditions of, the block parameter word is inside pipes |  | .  On the following line you set your condition or instructions for the array, followed by an ‘end’ to the iteration. You can also set up an iteration in one line code, your array .dot then your enumerable followed by curly brackets { |your block parameter|  then the condition/instructions}, this set up does not need the ‘do’ or  ‘end’ commands. 
     Example: 
letter_array.map do |letters|
    				 letters.upcase 
end 
 or 
		       letter_array.map {|letters| letters.upcase|} 

	That’s the basics of iteration. Further into coding, there’s more you can add, by chaining enumerables.  Or your array becoming larger and other conditions set to be met with other enumerables such as  ‘while’ looping statements. Iterating is an enormous part of coding.  

