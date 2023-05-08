Download Link: https://assignmentchef.com/product/solved-prog1970-assignment-1-crypto-magic
<br>
This assignment has you writing an encrypting / decrypting utility for Linux.  This utility will take any ASCII file and encrypt it in such a way that its contents are not readable – until they are decrypted by the utility.

<ul>

 <li>Practice creating a software project in Linux in the required development directory structure</li>

 <li>Practice creating a makefile for a Linux software project</li>

 <li>Reinforce C Programming techniques – File I/O using ASCII files, Command-Line Processing</li>

</ul>




<h1>Requirements</h1>

<ol>

 <li>The utility needs to be called <strong>cryptoMagic</strong> and needs to be written in C

  <ol>

   <li>The utility has 2 command-line switches – they are –encrypt and –decrypt</li>

   <li>If none of these switches is specified, then –encrypt is assumed</li>

   <li>The utility also takes the name of an <strong>ASCII input file</strong> to encrypt/decrypt as an argument. d. For example:</li>

  </ol></li>

</ol>

cryptoMagic –encrypt myFile.txt ß will encrypt the contents of the myFile.txt file cryptoMagic myFile.txt  ß will encrypt the contents of the myFile.txt file cryptoMagic –decrypt myFile.crp ß will decrypt the contents of the myFile.crp file

<ol start="2">

 <li>When the utility is asked to –encrypt an ASCII file, it will take the input filename and produce the encrypted file with the same <u>base filename</u> and an .crp file extension</li>

 <li>For example:</li>

</ol>

cryptoMagic –encrypt myFile.txt ß will produce an encrypted file called myFile.crp

<ol start="3">

 <li>When the utility is asked to –decrypt an encrypted file, it will take the input filename and produce the decrypted file with the same <u>base filename</u> and an .txt file extension</li>

 <li>For example:</li>

</ol>

cryptoMagic –decrypt myFile.crp ß will produce a decrypted file called myFile.txt

<ol start="4">

 <li>It should be noted that the <u>input file can have any file extension</u>. When asked to <em>encrypt</em>, you need to replace the existing file extension (if any) with .crp.  Similarly when asked to <em>decrypt</em>, you need to replace the existing file extension (if any) with .txt

  <ol>

   <li>Encrypting always produces a file with a .crp extension, decrypting always produces a file with a .txt extension</li>

   <li>Also note that you may be asked to encrypt or decrypt a file that has <u>no extension</u>! In this case, you have no existing extension to replace – you only need to append the .txt (if decrypting) and .crp (if encrypting)</li>

  </ol></li>

 <li>Each line (up to and including the carriage return (noted as <strong>&lt;CR&gt;</strong> below)) in the unencrypted ASCII file is guaranteed of being 120 characters of less. While processing the input ASCII file you need to process one line at a time.  Continue to process the input file until you reach the end of the file.

  <ol>

   <li>Please note that it is <u>not guaranteed</u> that each line actually ends in a carriage return … how will you handle that?</li>

  </ol></li>

 <li>The encryption scheme is applied to each character in the line:

  <ol>

   <li>If the character is a <strong>&lt;tab&gt;</strong> (ASCII value 9) then simply transform it into the output character sequence <strong>TT</strong>.</li>

   <li>The <strong>carriage return</strong> characters are <strong>not</strong> to be <strong>encrypted</strong> – they are left <u>as is</u> in the resultant output file (the <strong>&lt;CR&gt;</strong> in the example below is meant for illustration <strong><u>only</u></strong> – do not output “&lt;CR&gt;”)</li>

  </ol></li>

</ol>

<u>NOTE</u>: The term “carriage return” in this document does not apply to any specific ASCII code.  It applies to the typical                   end-of-line character that exists in TEXT files within the Linux OS.  You may want to investigate what constitutes a                   <em>carriage return</em> (i.e. end-of-line character in a TEXT file) in the Linux OS

<ol>

 <li>If is not a tab or a carriage return character, then apply the encryption scheme in steps d through f below</li>

 <li>Take the ASCII code for the input character and subtract a value of 16 from it. Let’s call this resultant value “outChar”</li>

 <li>If the resulting outChar value is less than 32, then another step must be taken: outChar = (outChar – 32) + 144</li>

 <li>You need to write the ASCII value of the new encrypted character (i.e. outChar) to the destination file as a <u>2 digit</u> <u>hexadecimal value</u>. Note that this will effectively double the length of the input line in terms of size … For example – if the input (unencrypted) file is:</li>

</ol>

Hello There how are you?<strong>&lt;CR&gt;</strong>

My name is Sean Clarke.<strong>&lt;tab&gt;</strong>I like software!<strong>&lt;CR&gt;</strong>

Then the encrypted file is:

38555C5C5F80445855625580585F678051625580695F652F<strong>&lt;CR&gt;</strong>

<h2>3D69805E515D55805963804355515E80335C51625B558E<strong>TT</strong>39805C595B5580635F56646751625581<strong>&lt;CR&gt;</strong></h2>

<ol start="7">

 <li>Each line (up to an including the carriage return (if it exists)) in the encrypted ASCII file is guaranteed of being less 255 characters or less. Remember – while processing the input ASCII file you need to process one line at a time.</li>

 <li>The decryption scheme is applied to each <u>pair of characters</u> in the input line:

  <ol>

   <li>You need to see if the pair of characters you are processing is the sequence <strong>TT</strong> – if so, then simply transform this pair of characters into a <strong>&lt;tab&gt;</strong> character (ASCII value 9) in the output file.</li>

   <li>If the pair of characters is not the sequence TT, then translate the first character of the pair by multiplying its <em>face value</em> by 16. Remember that hex values of A through F take on the <em>face values</em> of 10 through 15.  Then add the <em>face value</em> of the second character in the pair.  Let’s call the resulting value “outChar”.  For example:

    <ul>

     <li>Reading the pair of characters “38” from the encrypted file will translate into an outChar value of 56 decimal.</li>

     <li>Reading the pair of characters “5C” from the encrypted file will translate into an outChar value of 92 decimal. c. Now you need to add 16 to outChar.</li>

    </ul></li>

   <li>If the resulting outChar value is greater than 127, then another step must be taken: outChar = (outChar – 144) + 32</li>

   <li>The outChar value now contains the decrypted ASCII code for the character that you have just decoded. So take this decrypted character value (i.e. outChar) and write it to the destination file as a character.</li>

   <li>The <strong>carriage return</strong> characters are <strong>not</strong> to be <strong>decrypted</strong> – they are left as is in the resultant file.</li>

  </ol></li>

</ol>

For example – if the input (encrypted) file is:

4458596380555E5362696064595F5E80635358555D55805963806062556464698067555962548E<strong>&lt;CR&gt;</strong> 39635E87648059642F812F<strong>&lt;CR&gt;</strong>

Then the decrypted file is:

This encryption scheme is pretty weird.<strong> &lt;CR&gt;</strong> Isn’t it?!?<strong> &lt;CR&gt;</strong>

<ol start="9">

 <li>It is expected that your cryptoMagic utility has been tested (perhaps by using the above examples) as well as with any other encrypted / decrypted examples you can think of. Don’t forget about the extreme / boundary test cases!</li>

 <li>It is expected that your cryptoMagic utility has been designed using modular techniques (i.e. the program has been written using functions that you’ve created).

  <ol>

   <li>The solution must have at least 2 source files and 1 include file</li>

   <li>There should be no debugging messages present in your final submitted utility</li>

  </ol></li>

 <li>Your solution structure must include a makefile and also follow the recommended Linux development directory structure as outlined in the <u>Linux-Development-Project-Code-Structure</u> document within eConestoga.</li>

</ol>