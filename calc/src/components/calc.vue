<template>
<div class="Calc">
    <table>
        <tr>
            <th v-if="scientific==false" colspan="4" v-on:click="total++">{{total}}</th>
            <th v-else colspan="5" v-on:click="total++">{{total}}</th>
        </tr>
        <tr>
            <td v-if="scientific==false" v-on:click="scientific=switchScientific(scientific)">e π <br/> ln √</td>
            <td v-if="scientific==true" v-on:click="scientific=switchScientific(scientific)">+ - <br/>* /</td>
            <td v-on:click="total=0,num1=0,op=''">AC</td>
            <td v-on:click="total=del(total)">DEL</td>
            <td v-if="scientific==false" v-on:click="op='/'">/</td>
            <td v-if="scientific==true" v-on:click="total=set(total,Math.E,op)">e</td>
            <td v-if="scientific==true">log</td>
        </tr>
        <tr>
            <td v-on:click="total=set(total,1,op)">1</td>
            <td v-on:click="total=set(total,2,op)">2</td>
            <td v-on:click="total=set(total,3,op)">3</td>
            <td v-if="scientific==false" v-on:click="op='*'">*</td>
            <td v-if="scientific==true">ln</td>
            <td v-if="scientific==true">x^2</td>
        </tr>
        <tr>
            <td v-on:click="total=set(total,4,op)">4</td>
            <td v-on:click="total=set(total,5,op)">5</td>
            <td v-on:click="total=set(total,6,op)">6</td>
            <td v-if="scientific==false" v-on:click="op='+'">+</td>
            <td v-if="scientific==true" v-on:click="total=set(total,Math.PI,op)">π</td>
            <td v-if="scientific==true">mod</td>
        </tr>
        <tr>
            <td v-on:click="total=set(total,7,op)">7</td>
            <td v-on:click="total=set(total,8,op)">8</td>
            <td v-on:click="total=set(total,9,op)">9</td>
            <td v-if="scientific==false" v-on:click="op='-'">-</td>
            <td v-if="scientific==true">√</td>
            <td v-if="scientific==true">x^y</td>
        </tr>
        <tr>
            <td v-on:click="total=set(total,'.',op)">.</td>
            <td v-on:click="total=set(total,0,op)">0</td>
            <td colspan="2" v-on:click="total=equal(total,num1,op)">=</td>
            <td v-if="scientific==true">x!</td>
        </tr>
    </table>
    <div>
        <button v-on:click="debug(total,num1,op,scientific)">Debug</button>
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
            num1: 0,
            scientific: false
        }
    },
    methods :{
        del: function(number){
            var temp = number.toString();
            if(temp.length==1 || (temp.length==2 && temp.includes('-'))){
                return 0;
            }
            else{
                temp = temp.substring(0, temp.length-1);
                return parseInt(temp);                
            }

        },
        equal: function(total,num1,op){
            var temp=num1;
            switch(op){
                case "+":
                    this.op="";
                    this.num1=0;
                    return total+temp;
                case "/":
                    this.op="";
                    this.num1=0;
                    return total/temp;
                case "-":
                    this.op="";
                    this.num1=0;
                    return total-temp;
                case "*":
                    this.op="";
                    this.num1=0;
                    return total*temp;
            }
        },
        setTempNumber: function(number){
            if (this.num1==0){
                this.num1=number;
            }
            else{
                var new_number = number.toString();
                new_number+=number;
                this.num1=parseInt(new_number);
            }
            
        },        
        set: function(total,number,op){
            var new_number = total.toString();
            if(total==0 || (total==Math.E && op=="") || (total==Math.PI && op=="")){
                return number;
            }
            else if(number=='.' && !total.includes('.')){
                new_number+=number;
                return parseInt(new_number);                
            }
            else if (op==""){
                new_number+=number;
                return parseInt(new_number);
            }
            else{
                this.setTempNumber(number);
                return total;
            }
        },
        debug: (num1,total,op,scientific)=>{
            console.table([num1,total,op]);
            console.log(scientific)
        },
        switchScientific: (scientific)=>{
            switch(scientific){
                case true:
                    return false;
                case false:
                    return true;
            }
        }

    }
}
</script>

<style scoped>
table,td,th {
    border: 1px solid white;
    width:15px;
    height:15px;
    table-layout:auto;
    width: 300px;
    height: 30px;
    background-color:#42f5ce;
}

td:hover{
    background-color:#0673b8;
    color:white;
}

table{
    border-collapse:collapse;
    margin-left: auto;
    margin-right: auto;
}

button{
    margin-top:1%;
}
</style>