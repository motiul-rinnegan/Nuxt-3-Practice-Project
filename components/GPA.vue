<template>
    <div class="flex flex-col items-center py-0 justify-center">
        <div>
          <label class="flex flex-col items-center justify-center block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300 ">Enter percentage using comma</label>
          <input v-model="inputs" type="text" placeholder = "ex: 40,60,70,80,90" class="w-96 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required/>
        </div>
        <div class="flex flex-col items-center py-5 justify-center">
      <button  class="w-64 text-white bg-black hover:bg-gray-900 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-black dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700" @click="submit">Calculate</button>
       <button  class="w-64 text-white bg-black hover:bg-gray-900 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-black dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700" @click="onclick">Clear</button> 
        </div>
        
        <div v-if="showResult">
        <div class="w-64 overflow-x-auto relative">
        <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <tbody>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                    <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                        GPA
                    </th>
                    <td class="py-4 px-6">
                        {{average}}
                    </td>
                </tr>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                    <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                        Overall Percentage
                    </th>
                    <td class="py-4 px-6">
                        {{percentage}}
                    </td>
                </tr>
              <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                    <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                        Grade
                    </th>
                    <td class="py-4 px-6">
                        {{grade}}
                    </td>
                </tr>
                <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                    <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                        CGPA
                    </th>
                    <td class="py-4 px-6">
                        {{cgpa}}
                    </td>
                </tr>
              </tbody>
            </table>
        </div>
      </div>
    </div>
    </template>
    <script setup lang="ts">
    const inputs = ref('');
    const arr = ref([ ]);
    const average = ref<number>( );
    const cgpa = ref('');
    const grade = ref('');
    const percentage = ref('');
    const showResult = ref(false);
    function submit(){
    showResult.value = true;
      arr.value = inputs.value;
       let sum = 0;
       arr.value=arr.value.split(",");
       for (var i = 0; i < arr.value.length; i++) {
       sum += parseInt(arr.value[i], 10);
      }
      average.value = (((sum / 100)*4)/arr.value.length).toFixed(2);
      if (average.value<1.0 ){
        grade.value = "Not Found";
        percentage.value = "Not Found";
        cgpa.value = "Not Found";
      }
      else if (average.value==1.0){
        grade.value = "D";
        percentage.value = "65-66%";
        cgpa.value = "6.8-6.9"; 
      }
      else if(average.value<=1.3){
        grade.value = "D+";
        percentage.value = "67-69%";
        cgpa.value = "7.0-7.2"; 
      }
      else if(average.value<=1.7){
        grade.value = "C-";
        percentage.value = "70-72%";
        cgpa.value = "7.3-7.5"; 
      }
      else if(average.value<=2.0){
        grade.value = "C";
        percentage.value = "73-76%";
        cgpa.value = "7.6-8.0"; 
      }
      else if(average.value<=2.3){
        grade.value = "C+";
        percentage.value = "77-79%";
        cgpa.value = "8.1-8.3"; 
      }
      else if(average.value<=2.7){
        grade.value = "B-";
        percentage.value = "80-82%";
        cgpa.value = "8.4-8.6"; 
      }
      else if(average.value<=3.0){
        grade.value = "B";
        percentage.value = "83-86%";
        cgpa.value = "8.7-9.0"; 
      }
      else if(average.value<=3.3){
        grade.value = "B+";
        percentage.value = "87-89%";
        cgpa.value = "9.1-9.3"; 
      }
      else if(average.value<=3.7){
        grade.value = "A-";
        percentage.value = "90-92%";
        cgpa.value = "9.4-9.6"; 
      }
      else if(average.value<4.0){
        grade.value = "A";
        percentage.value = "93-96%";
        cgpa.value = "9.7-10.0"; 
      }
      else if(average.value==4.0){
        grade.value = "A+";
        percentage.value = "97-100%";
        cgpa.value = "10.0"; 
      }
      }
      function onclick(){
       showResult.value = false;
       inputs.value = '';
    }
    </script>
    