<html>
    <head>
        <title>Hamming code</title>
        <script>
            function code(){
                let input = document.getElementById('message').value;
                input = input.split('');
                for(let i = 0; i < input.length; i++)
                    input[i] *= 1;
                let control = new Array();
                control.push((input[0] + input[1] + input[3]) % 2);
                control.push((input[0] + input[2] + input[3]) % 2);
                control.push((input[1] + input[2] + input[3]) % 2);
                input.splice(0, 0, control[0]);
                input.splice(1, 0, control[1]);
                input.splice(3, 0, control[2]);
                document.getElementById('codedmessage').value = input.join('');
            }
            
            function decode()
			{
                let input = document.getElementById('codedmessage').value;
                input = input.split('');
                for(let i = 0; i < input.length; i++)
				{
                    input[i] *= 1;
				}
                
                let control = new Array();
                let bitOfError = 0;
                control.push((input[2] + input[4] + input[6]) % 2);
                control.push((input[2] + input[5] + input[6]) % 2);
                control.push((input[4] + input[5] + input[6]) % 2);
                let inpControl = new Array();
                inpControl.push(input[0]);
                inpControl.push(input[1]);
                inpControl.push(input[3]);
                for (let i = 0; i < control.length; i++)
				{
                    if (inpControl[i] != control[i])
					{
                        bitOfError += Math.pow(2, i);
					}
                }
                if (bitOfError == 0)
				{             
                    document.getElementById('placeOfError').textContent = 'No error';
                    input.splice(0, 2);
                    input.splice(1, 1);
                    document.getElementById('decodedmessage').value = input.join('');
                }
                else 
				{
                    document.getElementById('placeOfError').textContent = 'Error at ' + bitOfError;
                    input[bitOfError - 1] = (input[bitOfError - 1] + 1) % 2;
                    input.splice(0, 2);
                    input.splice(1, 1);
                    document.getElementById('decodedmessage').value = input.join('');
                }
            }
        </script>
    </head>
    <body>
        <h1>Hamming code</h1>
        <p> <input type='text' id='message'> Type the message </p>
        <p> <input type='button' value='code' onClick='code()'> </p>
        <p> <input type='text' id='codedmessage'> Coded message </p>
        <p> <input type='button' value='decode' onClick='decode()'> </p>
        <p> <input type='text' id='decodedmessage'> Decoded message </p>
        <p> <span id='placeOfError'> </span> </p>
    </body>
</html>
