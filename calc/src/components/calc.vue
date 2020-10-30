<template>
<div class="Calc">
    <table>
        <tr>
            <th v-if="scientific==false" colspan="4" v-on:click="total++">{{total}} {{op}}
                <span v-if="num1!=''">{{num1}}</span>
            </th>
            <th v-else colspan="5" v-on:click="total++">{{total}} {{op}}
                <span v-if="num1!=''">{{num1}}</span>
            </th>
        </tr>
        <tr>
            <td v-if="scientific==false" v-on:click="scientific=switchScientific(scientific)">e π <br/> ln √</td>
            <td v-if="scientific==true" v-on:click="scientific=switchScientific(scientific)">+ - <br/>* /</td>
            <td v-on:click="total=0,num1=0,op=''">AC</td>
            <td v-on:click="total=del(total,op,num1)[0], op=del(total,op,num1)[1],num1=del(total,op,num1)[2]">DEL</td>
            <td v-if="scientific==false" v-on:click="op='/'">/</td>
            <td v-if="scientific==true" v-on:click="total=set(total,Math.E,op)">e</td>
            <td v-if="scientific==true" v-on:click="op='log'">log</td>
        </tr>
        <tr>
            <td v-on:click="total=set(total,1,op)">1</td>
            <td v-on:click="total=set(total,2,op)">2</td>
            <td v-on:click="total=set(total,3,op)">3</td>
            <td v-if="scientific==false" v-on:click="op='*'">*</td>
            <td v-if="scientific==true" v-on:click="total=equal(total,0,'ln')">ln</td>
            <td v-if="scientific==true" v-on:click="total=equal(total,0,'sqr')">x^2</td>
        </tr>
        <tr>
            <td v-on:click="total=set(total,4,op)">4</td>
            <td v-on:click="total=set(total,5,op)">5</td>
            <td v-on:click="total=set(total,6,op)">6</td>
            <td v-if="scientific==false" v-on:click="op='+'">+</td>
            <td v-if="scientific==true" v-on:click="total=set(total,Math.PI,op)">π</td>
            <td v-if="scientific==true" v-on:click="op='%'">mod</td>
        </tr>
        <tr>
            <td v-on:click="total=set(total,7,op)">7</td>
            <td v-on:click="total=set(total,8,op)">8</td>
            <td v-on:click="total=set(total,9,op)">9</td>
            <td v-if="scientific==false" v-on:click="op='-'">-</td>
            <td v-if="scientific==true" v-on:click="total=equal(total,0,'sqrt')">√</td>
            <td v-if="scientific==true" v-on:click="op='^'">x^y</td>
        </tr>
        <tr>
            <td v-on:click="total=set(total,'.',op)">.</td>
            <td v-on:click="total=set(total,0,op)">0</td>
            <td colspan="2" v-on:click="total=equal(total,num1,op)">=</td>
            <td v-if="scientific==true" v-on:click="total=factorial(total)">x!</td>
        </tr>
    </table>
    <div>
        <div>
            <p> <strong> This calculator only supports 2-variable calculations. <br/><br/></strong> If you encounter an unwanted problem,
            click the Debug button below to find out what's wrong.</p>
        </div>
        <button v-on:click="debug(total,num1,op,scientific,showMessage), showMessage=message(showMessage)">Debug</button>
        <div v-if="showMessage==true">
            <p>Check your console!<br/> Click the button again to clear your console.</p>
        </div>
    </div>
</div>

</template>


<script>

export default {
    name: 'Calc',
    components:{

    },
    data(){
        return{
            total: 0,
            op: "",
            num1: "",
            scientific: false,
            showMessage: false
        }
    },
    methods :{
        del: function(number,op,num1){
            var temp = number.toString();
            var temp_num1 = num1.toString();
            if (op=="" && num1==""){
                if(temp.length==1 || (temp.length==2 && temp.includes('-'))){
                    temp=0;
                }
                else{
                    temp = temp.substring(0, temp.length-1);                
                }
            }
            else if (op!="" && num1==""){
                op=""
            }
            else if (number!="0" && op!=""){
                if(temp_num1.length==1 || (temp_num1.length==2 && temp_num1.includes('-'))){
                    temp_num1="";
                }
                else{
                    temp_num1 = temp_num1.substring(0, temp_num1.length-1);                
                }                
            }
            return [temp,op,temp_num1];


        },
        equal: function(total,num1,op){
            total=Number(total);
            var temp=Number(num1);
            switch(op){
                case "+":
                    this.op="";
                    this.num1='';
                    return total+temp;
                case "/":
                    this.op="";
                    this.num1='';
                    return total/temp;
                case "-":
                    this.op="";
                    this.num1='';
                    return total-temp;
                case "*":
                    this.op="";
                    this.num1='';
                    return total*temp;
                case "sqrt":
                    this.op="";
                    this.num1='';
                    return Math.sqrt(total);
                case "sqr":
                    this.op="";
                    this.num1='';
                    return Math.pow(total,2);
                case "%":
                    this.op="";
                    this.num1='';
                    return total%temp;
                case "^":
                    this.op="";
                    this.num1='';
                    return Math.pow(total,temp); 
                case "log":
                    this.op="";
                    this.num1='';
                    return Math.log(temp)/Math.log(total);
                case "ln":
                    this.op="";
                    this.num1='';
                    return Math.log(total);                                                                            
            }
        },
        setTempNumber: function(number){
            var new_number = number.toString();            
            if (this.num1==""){
                this.num1=number;
            }
            else if(number=='.' && !new_number.includes('.')){
                this.num1+=(new_number);                 
            }
            else {
                this.num1+=(new_number);
            }
            
        },        
        set: function(total,number,op){
            var new_number = total.toString();            
            if((total==0) || (total==Math.E && op=="") || (total==Math.PI && op=="")){
                return number;
            }
            /* Adding decimal point*/
            else if(number=='.' && !new_number.includes('.') && op==""){
                new_number+='.';
                return (new_number);                
            }            
            else if (op==""){
                new_number+=number;
                return (new_number);
            }
            else{
                this.setTempNumber(number);
                return total;
            }
        },
        debug: (num1,total,op,scientific,showMessage)=>{
            if (showMessage){
                console.clear();
            }
            else{
                var objectDebug = {
                    Total_Number : total,
                    Second_Number : num1,
                    Operation: op,
                    Is_Scientific : scientific,
                }
                console.table(objectDebug);                  
            }
              

        },
        switchScientific: (scientific)=>{
            switch(scientific){
                case true:
                    return false;
                case false:
                    return true;
            }
        },
        factorial: (number)=>{
            if (number==0 || number==1){
                return 1;
            }
            else{
                var temp_number=number;
                while(temp_number>1){
                    temp_number--;
                    number=number*temp_number;                    
                }
                return number;
            }
        },
        message: (showMessage)=>{
            if (showMessage){
                return false;
            }
            else{
                return true;
            }
        }

    }
}
</script>

<style scoped>

th{
    background-color:#99E1D9;
    border: 1px solid white;
    width:15px;
    height:15px;
    table-layout:auto;
    width: 300px;
    height: 50px;
    justify-content: space-between;
}

table,td {
    border: 1px solid white;
    width:15px;
    height:15px;
    table-layout:auto;
    width: 350px;
    height: 50px;
    background-color:#42f5ce;
    justify-content: space-between;
}



td:hover{
    background-color:#0673b8;
    color:white;
}

th:hover{
    background-color:#2191FB;
}

table{
    border-collapse:collapse;
    margin-left: auto;
    margin-right: auto;
}

button{
    font-family: 'Lato', sans-serif ;
    margin-top:0.5%;
    background-color: #f57e00;
    border: 2px solid #f57e00;
    color: black;
    font-size:1rem;
    padding: 10px 16px;
    text-align: center;
    display: inline-block;
    transition-duration: 0.4s;
    cursor: pointer;
    border-radius:5%;
}
button:hover{
    background-color: white;
    color:#f57e00;
    border: 2px solid #f57e00;
}
</style>