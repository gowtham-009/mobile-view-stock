<template>
      <Toast />
    <div>
      <div  class="w-full" v-if="loading">
    <div class="p-1 space-y-4">
    <!-- Table Skeleton -->

    <div class="border border-gray-200 rounded-lg ">

      <div class="h-20   bg-white animate-pulse rounded-lg flex gap-2 justify-end items-center py-5 p-3">
      <div class="h-12 w-96 bg-gray-200 animate-pulse rounded"></div>
      <div class="h-12 w-8 bg-gray-200 animate-pulse rounded"></div>
      <div class="h-12 w-8 bg-gray-200 animate-pulse rounded"></div>
    </div>

        <div class="grid grid-cols-2 bg-gray-100 p-3 font-semibold">
            <div class="h-8 w-20 bg-gray-200 animate-pulse rounded"></div>
            <div class="h-8 w-20 bg-gray-200 animate-pulse rounded"></div>
            
        </div>

        <!-- Table Rows -->
        <div class="divide-y divide-gray-200">
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
               
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
               
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
               
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
              
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
               
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
               
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
              
            </div>
            <div class="grid grid-cols-2 p-3 animate-pulse">
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
                <div class="h-6 w-20 bg-gray-200 rounded"></div>
               
            </div>
            
        </div>
    </div>

    <!-- Pagination Skeleton -->
    <div class="flex justify-center space-x-2">
        <div class="h-8 w-8 bg-gray-200 animate-pulse rounded-full"></div>
        <div class="h-8 w-8 bg-gray-200 animate-pulse rounded-full"></div>
        <div class="h-8 w-8 bg-gray-200 animate-pulse rounded-full"></div>
    </div>
</div>
</div>
      <div class="p-1 w-full" v-if="content">
        
      
       
  
        <div class="w-full p-2  mt-2" >
            <DataTable ref="dt" v-model:filters="filters" :value="customers" paginator showGridlines :rows="10" dataKey="id"
            filterDisplay="menu" :loading="loading" :globalFilterFields="['account', 'bank', 'date']" stripedRows   >
              <template #header>
                <div class="w-full flex justify-end items-center">
                    <IconField>
                        <InputIcon>
                            <i class="pi pi-search " />
                        </InputIcon>
                        <InputText v-model="filters['global'].value" placeholder="Search stock and company"  />
                    </IconField>
                    <MultiSelect
                v-model="selectedColumns"
                :options="columns"
                optionLabel="header"
                @change="updateVisibleColumns"
                display="template"
  
                :showToggleAll="false"
                :dropdownIcon="null" 
               class="p-0 text-white ml-2"
                style="width: 40px; height: 34px; "
                >
  
                <template #dropdownicon>
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6 text-slate-500">
                    <path fill-rule="evenodd" d="M1.5 5.625c0-1.036.84-1.875 1.875-1.875h17.25c1.035 0 1.875.84 1.875 1.875v12.75c0 1.035-.84 1.875-1.875 1.875H3.375A1.875 1.875 0 0 1 1.5 18.375V5.625ZM21 9.375A.375.375 0 0 0 20.625 9h-7.5a.375.375 0 0 0-.375.375v1.5c0 .207.168.375.375.375h7.5a.375.375 0 0 0 .375-.375v-1.5Zm0 3.75a.375.375 0 0 0-.375-.375h-7.5a.375.375 0 0 0-.375.375v1.5c0 .207.168.375.375.375h7.5a.375.375 0 0 0 .375-.375v-1.5Zm0 3.75a.375.375 0 0 0-.375-.375h-7.5a.375.375 0 0 0-.375.375v1.5c0 .207.168.375.375.375h7.5a.375.375 0 0 0 .375-.375v-1.5ZM10.875 18.75a.375.375 0 0 0 .375-.375v-1.5a.375.375 0 0 0-.375-.375h-7.5a.375.375 0 0 0-.375.375v1.5c0 .207.168.375.375.375h7.5ZM3.375 15h7.5a.375.375 0 0 0 .375-.375v-1.5a.375.375 0 0 0-.375-.375h-7.5a.375.375 0 0 0-.375.375v1.5c0 .207.168.375.375.375Zm0-3.75h7.5a.375.375 0 0 0 .375-.375v-1.5A.375.375 0 0 0 10.875 9h-7.5A.375.375 0 0 0 3 9.375v1.5c0 .207.168.375.375.375Z" clip-rule="evenodd" />
                    </svg>

              </template>
                
                <template #footer v-if="showReset">
                  <button type="button"  @click="resetColumns" class="rounded-md w-full bg-indigo-600 px-2 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Reset</button>
  
                </template>
                </MultiSelect>
                <button type="button"  @click="exportCSV($event)" class="rounded-md ml-2  px-1 py-1 text-sm font-semibold text-slate-500  border-2"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
                <path fill-rule="evenodd" d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25Zm-.53 14.03a.75.75 0 0 0 1.06 0l3-3a.75.75 0 1 0-1.06-1.06l-1.72 1.72V8.25a.75.75 0 0 0-1.5 0v5.69l-1.72-1.72a.75.75 0 0 0-1.06 1.06l3 3Z" clip-rule="evenodd" />
                </svg>
                </button>
                </div>
              </template>
            <template #empty> No customers found. </template>
            <template #loading> Loading customers data. Please wait. </template>
  
            <Column v-if="visibleColumns.includes('account')" field="account" sortable header="Account">
                <template #body="{ data }">
                   <span  @click="topcanva(data)"> {{ data.account }}</span>
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('bank')" field="bank" sortable header="Bank">
                <template #body="{ data }">
                  <span  @click="topcanva(data)">  {{ data.bank }}</span>
                </template>
                <template #filter="{ filterModel }">
                    <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
                </template>
            </Column>
            <Column v-if="visibleColumns.includes('date')" header="Date" filterField="date" dataType="date">
                <template #body="{ data }">
                <span  @click="topcanva(data)">{{ formatDatee(data.date) }}</span>
                    </template>
                    <template  #filter="{ filterModel }">
                        <DatePicker 
                        v-model="filters.date.constraints[0].value" 
                        dateFormat="dd-mm-yy" 
                        showIcon
                        @update:modelValue="applyDateFilter"
                />
                </template>
            </Column>
            
           
        </DataTable>


  
        <Drawer v-model:visible="visibleTop2" header="Stock Details" position="top" style="height: auto">

<div class="w-full p-1 mt-2" >
      <hr>
       <div class="w-full p-1">
        <span class="text-lg"><b>CRM123MH3456</b></span>
        <hr>

        <div class="w-full p-1 flex justify-center items-center gap-2">
          <div class="bg-slate-400 p-3 rounded-full" style="width: 35px; height: 35px;"></div>
          <span>{{ account }}</span>
        </div>
       </div>
       <div class="w-full mt-2">
      
      <Accordion value="0">
  <AccordionPanel value="0">
      <AccordionHeader>Details</AccordionHeader>
      <AccordionContent>
  
        <div class="w-full  flex">
          <div class="w-full " ><span>Account</span></div>
          <div class="w-full " ><span>{{account}}</span></div>
        </div>
        <div class="w-full  flex">
          <div class="w-full " ><span>Bank</span></div>
          <div class="w-full " ><span>{{bank}}</span></div>
        </div>
        <div class="w-full  flex">
          <div class="w-full " ><span>Date</span></div>
          <div class="w-full " ><span>{{date}}{{ time }}</span></div>
        </div>
        <div class="w-full  flex">
          <div class="w-full " ><span>Amount</span></div>
          <div class="w-full " ><span>{{amount}}</span></div>
        </div>
        <div class="w-full  flex">
          <div class="w-full " ><span>Status</span></div>
          <div class="w-full " ><span>{{status}}</span></div>
        </div>
       
       
         
      </AccordionContent>
  </AccordionPanel>
  </Accordion>
      </div>
  
    </div>
<!-- Mobile Select Dropdown -->
<div class="flex items-center sm:hidden rounded-lg p-1" style="border: 1px solid gainsboro;">
    <select
      v-model="selectedTab"
      aria-label="Select a tab"
      class="col-start-1 row-start-1 w-full outline-none appearance-none rounded-md bg-white py-2 pl-3 pr-8 text-base text-gray-900   "
    >
      <option  value="activity"> Activity</option>
      <option value="email">Email</option>
      <option value="comments">Comments</option>
      <option value="data">Data</option>
      <option value="tasks">Tasks</option>
      <option value="notes">Notes</option>
      <option value="attaching">Attachements</option>
    </select>
    <i class="pi pi-angle-down"></i>
  </div>

  <!-- Desktop Tabs -->
  <div class="hidden sm:block">
    <div class="border-b border-gray-200">
      <nav class="-mb-px flex space-x-8" aria-label="Tabs">
        <a
          href="#"
          @click.prevent="changeTab('activity')"
          :class="[
            selectedTab === 'activity'
              ? 'border-indigo-500 text-indigo-600'
              : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700',
            'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium'
          ]"
        >
        <i class="pi pi-asterisk"></i>  Activity
        </a>

        <a
          href="#"
          @click.prevent="changeTab('email')"
          :class="[
            selectedTab === 'email'
              ? 'border-indigo-500 text-indigo-600'
              : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700',
            'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium'
          ]"
        >
        <i class="pi pi-envelope"></i>  Email
        </a>

        <a
          href="#"
          @click.prevent="changeTab('comments')"
          :class="[
            selectedTab === 'comments'
              ? 'border-indigo-500 text-indigo-600'
              : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700',
            'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium'
          ]"
        >
        <i class="pi pi-comments"></i>  Comments
        </a>

        <a
          href="#"
          @click.prevent="changeTab('data')"
          :class="[
            selectedTab === 'data'
              ? 'border-indigo-500 text-indigo-600'
              : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700',
            'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium'
          ]"
        >
        <i class="pi pi-calendar"></i> Data
        </a>

        <a
          href="#"
          @click.prevent="changeTab('tasks')"
          :class="[
            selectedTab === 'tasks'
              ? 'border-indigo-500 text-indigo-600'
              : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700',
            'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium'
          ]"
        >
        <i class="pi pi-list-check"></i> Tasks
        </a>

        <a
          href="#"
          @click.prevent="changeTab('notes')"
          :class="[
            selectedTab === 'notes'
              ? 'border-indigo-500 text-indigo-600'
              : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700',
            'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium'
          ]"
        >
        <i class="pi pi-clipboard"></i>  Notes
        </a>
        <a
          href="#"
          @click.prevent="changeTab('attaching')"
          :class="[
            selectedTab === 'attaching'
              ? 'border-indigo-500 text-indigo-600'
              : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700',
            'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium'
          ]"
        >
        <i class="pi pi-link"></i>  Attachements
        </a>
      </nav>
     
    </div>
  </div>

  <div class="mt-2 p-1 " v-if="selectedTab === 'activity'">
      <h2 class="text-sm ">Activity</h2>
    </div>
    <div class="mt-2 p-1 " v-if="selectedTab === 'email'">
      <h2 class="text-sm ">Email</h2>
    </div>
    <div class="mt-2 p-1 " v-if="selectedTab === 'comments'">
      <h2 class="text-sm ">Comments</h2>
    </div>
    <div class="mt-2 p-1 " v-if="selectedTab === 'data'">
      <h2 class="text-sm ">Data</h2>
    </div>
    <div class="mt-2 p-1 " v-if="selectedTab === 'tasks'">
      <h2 class="text-sm ">Tasks</h2>
    </div>
     <div class="mt-2 p-1 " v-if="selectedTab === 'notes'">
      <h2 class="text-sm ">Notes</h2>
    </div>
    <div class="mt-2 p-1 " v-if="selectedTab === 'attaching'">
      <h2 class="text-sm ">Attaching</h2>
    </div>




    <div class="w-full p-1 flex justify-center gap-3" >
      <Button label="Proceed" severity="success" @click="proceedfun" raised />
      <Button label="Cancel" severity="danger" @click="cancelfun" variant="outlined" />
    </div>
</Drawer>


        

        </div>


        
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { onMounted } from 'vue';
  import DatePicker from 'primevue/datepicker';
  import { FilterMatchMode, FilterOperator } from '@primevue/core/api';
  import { useToast } from "primevue/usetoast";
  import 'primeicons/primeicons.css'
  import { useConfirm } from "primevue/useconfirm";

  const selectedTab = ref('activity');
const changeTab = (tab) => {
  selectedTab.value = tab;
};

  const loading=ref(true)
  const content=ref(false)








  const filters = ref();
const customers=ref([])
const getdata = async () => {
    try {
      const res = await fetch('/fadded.json');
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
      customers.value = await res.json();
      
    } catch (error) {
      console.error('Error:', error.message);
    }
  };
onMounted(() => {
    getdata()
    setInterval(() => {
      loading.value=false
      content.value=true
    }, 2000);
});


const initFilters = () => {
    filters.value = {
        global: { value: null, matchMode: FilterMatchMode.CONTAINS },
        account: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        bank: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        date: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.EQUALS }] },
       
    };
};


initFilters();

const applyDateFilter = () => {
if (filters.value.date.constraints[0].value) {
let selectedDate = filters.value.date.constraints[0].value;
filters.value.date.constraints[0].value = formatDate(selectedDate);
}
};

const formatDate = (date) => {
if (!date) return null;
const d = new Date(date);
return `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, "0")}-${String(d.getDate()).padStart(2, "0")}`;
};

const formatDatee = (dateString) => {
  if (!dateString) return "";
  const [year, month, day] = dateString.split("-");
  return `${day}-${month}-${year.slice(-4)}`; // Convert yy-mm-dd to dd-mm-yy
};



const columns = ref([
{ field: 'account', header: 'Account' },
{ field: 'bank', header: 'Bank' },
{ field: 'date', header: 'Date' },


]);

const selectedColumns = ref(columns.value.filter(col => ![ 'date'].includes(col.field)));
const visibleColumns = ref(selectedColumns.value.map(col => col.field)); // Tracks visibility
const showReset = ref(true); // Ensure reset is visible as some columns are unchecked initially

const updateVisibleColumns = () => {
visibleColumns.value = selectedColumns.value.map(col => col.field);
showReset.value = selectedColumns.value.length < columns.value.length; // Show Reset only when some columns are unchecked
};

const resetColumns = () => {
selectedColumns.value = columns.value.slice(); // Reset to all columns selected
updateVisibleColumns(); // Ensure UI updates
};

watch(selectedColumns, updateVisibleColumns, { deep: true });

const dt = ref();

const exportCSV = () => {
dt.value.exportCSV();
};



const visibleTop2 = ref(false);
const account=ref('')
const bank=ref('')
const date=ref('')
const time=ref('')
const amount=ref('')
const status=ref('')



const topcanva =(dataval)=>{
  visibleTop2.value=true
  account.value=dataval.account
bank.value=dataval.bank
date.value=dataval.date
time.value=dataval.time
amount.value=dataval.amount
status.value=dataval.status
}

const proceedfun=async()=>{
const formdata=new FormData()
formdata.append('account', account.value)
formdata.append('bank', bank.value)
formdata.append('date', date.value)
formdata.append('time', time.value)
formdata.append('amount', amount.value)
formdata.append('status', status.value)

const api='https://fakestoreapi.com/products'
try {
const res = await fetch(api,{
method:'POST',
body:formdata
});
if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
const data = await res.json();
toast.add({ severity: 'success', summary: 'Success Message', detail: data.id, life: 3000 });
} catch (error) {
console.error("Error:", error.message);
}


}

const cancelfun=async()=>{
const formdata=new FormData()
formdata.append('account', account.value)
formdata.append('bank', bank.value)
formdata.append('date', date.value)
formdata.append('time', time.value)
formdata.append('amount', amount.value)
formdata.append('status', status.value)
const api='https://fakestoreapi.com/products'
try {
const res = await fetch(api,{
method:'POST',
body:formdata
});
if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
const data = await res.json();
toast.add({ severity: 'error', summary: 'Cancel Message', detail: data.id, life: 3000 });
} catch (error) {
console.error("Error:", error.message);
}
}


  </script>
  
  <style >
  .p-checkbox-checked.p-variant-filled .p-checkbox-box{
    background-color: blue !important;
    border: blue !important;
  }
 
  .p-multiselect.p-variant-filled{
    background: none !important;
   
  }
  .p-multiselect-dropdown{
    border: 2px solid rgb(227, 227, 227);
    border-radius: 5px;
  }
  .p-multiselect{
  
    box-shadow: none !important;
  }
  </style>
  