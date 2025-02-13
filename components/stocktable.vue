<template>
  <Toast />



  <div class="overflow-hidden rounded-lg bg-white ">
    <div class="px-1 py-2 ">
      <div class="card flex justify-between items-center gap-2  text-lg">
       
       <div class="w-full">
        <div class="w-full text-black-400 text-md" > Statement For</div>
        <div class="w-full text-indigo-500 " style=" margin-top: -8px; font-size:10px;"> {{ startdate }} To {{ enddate }}</div>
       </div>
        <div class="w-full h-9  flex gap-2 justify-end" >

          <MultiSelect
              v-model="selectedColumns"
              :options="columns"
              optionLabel="header"
              @change="updateVisibleColumns"
              display="template"

              :showToggleAll="false"
              :dropdownIcon="null" 
              class="p-0 bg-indigo-500"
              style="width: 42px;"
            
             
              >
              <template #dropdownicon>
        <i class="pi pi-objects-column " />
    </template>
           
              <template #footer v-if="showReset">

              <Button label="Reset" style="width: 100%;" @click="resetColumns"/>
              </template>
              </MultiSelect> 
              <button type="button"  @click="customtoggle()" class="rounded-md bg-indigo-600 px-2 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"><i class="pi pi-filter-fill"></i></button>

              <button type="button"   @click="exportCSV($event)" class="rounded-md bg-indigo-600 px-2 py-1 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"><i class="pi pi-arrow-down"></i></button>

        </div>
         <div >
       

            
          <Drawer v-model:visible="visibleTop" header="Filter" position="top" style="height: auto">
            <span class="text-lg"><i class="pi pi-clock"></i> Frequently used time period</span>
      <div class="w-full p-1 flex gap-2 pl-5">
        <button type="button" :class="{ 'bg-indigo-600 text-white': activeFilter === 'week' }" class="rounded-md  px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300" @click="filterLastWeek" >7 Days</button>
        <button type="button" :class="{ 'bg-indigo-600 text-white': activeFilter === '15days' }" class="rounded-md   px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300" @click="filterLast15Days">15 Days</button>
        <button type="button" :class="{ 'bg-indigo-600 text-white': activeFilter === 'month' }" class="rounded-md  px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300" @click="filterLastMonth">Month</button>
        <button type="button" :class="{ 'bg-indigo-600 text-white': activeFilter === '3months' }" class="rounded-md  px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300" @click="filterLast3Months">3 Months</button>

      </div>

    <div class="mt-3">
      <span class="text-lg mt-3"><i class="pi pi-calendar"></i> Date Range Filter</span>
      <div class="w-full p-1  pl-5" >
       <div class="flex justify-center items-center gap-2">
        <div>
              <span>Start Date</span>
              <DatePicker  v-model="start" dateFormat="dd-mm-yy" showIcon />
          </div>
          <span>To</span>
          <div>
              <span>End Date</span>
              <DatePicker v-model="end" dateFormat="dd-mm-yy" showIcon />
          </div>
       </div>
      <div class="w-full flex justify-start mt-2">
        <button @click="applyFilter" class="text-white bg-indigo-600 py-1 px-2 rounded-lg">Apply filter</button>
      </div>
      </div>
    </div>
          </Drawer>

         </div>
  

        
      </div>
    </div>
  </div>

  
  <div class="w-full" v-if="loading" >

<div class="p-1 space-y-4">
  <ul role="list" class="grid grid-cols-2 gap-2 sm:grid-cols-2 lg:grid-cols-2 xs:grid-cols-1">
    
    <li class="col-span-1 rounded-lg bg-white shadow animate-pulse">
      <div class="flex w-full items-center justify-between space-x-6 p-2">
        <div class="flex truncate">
          <div class="flex justify-center items-center p-3 bg-indigo-50 rounded-full w-12 h-12"></div>
          <div class="w-full p-1">
            <div class="h-3 bg-gray-300 rounded w-24"></div>
            <div class="h-4 bg-gray-300 rounded w-16 mt-1"></div>
          </div>
        </div>
      </div>
    </li>

    <li class="col-span-1 rounded-lg bg-white shadow animate-pulse">
      <div class="flex w-full items-center justify-between space-x-6 p-2">
        <div class="flex truncate">
          <div class="flex justify-center items-center p-3 bg-indigo-50 rounded-full w-12 h-12"></div>
          <div class="w-full p-1">
            <div class="h-3 bg-gray-300 rounded w-24"></div>
            <div class="h-4 bg-gray-300 rounded w-16 mt-1"></div>
          </div>
        </div>
      </div>
    </li>

    <li class="col-span-1 rounded-lg bg-white shadow animate-pulse">
      <div class="flex w-full items-center justify-between space-x-6 p-2">
        <div class="flex truncate">
          <div class="flex justify-center items-center p-3 bg-green-50 rounded-full w-12 h-12"></div>
          <div class="w-full p-1">
            <div class="h-3 bg-gray-300 rounded w-24"></div>
            <div class="h-4 bg-gray-300 rounded w-16 mt-1"></div>
          </div>
        </div>
      </div>
    </li>

    <li class="col-span-1 rounded-lg bg-white shadow animate-pulse">
      <div class="flex w-full items-center justify-between space-x-6 p-2">
        <div class="flex truncate">
          <div class="flex justify-center items-center p-3 bg-green-50 rounded-full w-12 h-12"></div>
          <div class="w-full p-1">
            <div class="h-3 bg-gray-300 rounded w-24"></div>
            <div class="h-4 bg-gray-300 rounded w-16 mt-1"></div>
          </div>
        </div>
      </div>
    </li>

  </ul>


<!-- Table Skeleton -->
<div class="border border-gray-300 ">

<div class="h-10 p-2   animate-pulse">
<div class="h-6 bg-gray-200 rounded w-full animate-pulse"></div>
</div>

<div class="grid grid-cols-3 p-3 bg-gray-100">
  <div class="h-8 bg-gray-200 rounded w-24 animate-pulse"></div>
  <div class="h-8 bg-gray-200 rounded w-24 animate-pulse"></div>
  <div class="h-8 bg-gray-200 rounded w-16 animate-pulse"></div>
</div>

<div class="space-y-2">
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>
  <div class="grid grid-cols-3 p-3 border-t border-gray-300">
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-24 animate-pulse"></div>
    <div class="h-6 bg-gray-200 rounded w-10 animate-pulse"></div>
  </div>

</div>
</div>

<!-- Pagination Skeleton -->
<div class="flex justify-center space-x-2 mt-4">
<div class="h-8 w-8 bg-gray-200 rounded-full animate-pulse"></div>
<div class="h-8 w-8 bg-gray-200 rounded-full animate-pulse"></div>
<div class="h-8 w-8 bg-gray-200 rounded-full animate-pulse"></div>
</div>
</div>


</div>

<div class="w-full" v-if="content">
<div class="overflow-hidden rounded-lg bg-white ">
    <div class="px-1 py-1">
      <ul role="list" class="grid grid-cols-2 gap-2 sm:grid-cols-2 lg:grid-cols-2 xs:grid-cols-1">

<li ref="listItem" class="col-span-1  rounded-lg bg-white shadow">
<div class="flex w-full items-center justify-between space-x-6 p-2">
<div class="flex truncate">
  <div class="flex justify-center items-center p-3 bg-indigo-50 rounded-full"  >
         <img src="https://cdn-icons-png.flaticon.com/128/16416/16416833.png" alt="" width="30" height="30">
     </div>
     <div class="w-full p-1" >
         <span class="text-slate-400 text-xs">Invested Amount</span>
        <p class="text-slate-700 text-xs"> <span><i class="pi pi-indian-rupee" style="font-size: 12px;"></i></span> <span >{{ investamount }}</span></p>
     </div>
</div>
</div>
<div>

</div>
</li>

<li class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow">
<div class="flex w-full items-center justify-between space-x-6 p-2">
<div class="flex truncate">
<div class="flex justify-center items-center p-3 bg-indigo-50 rounded-full"  >
         <img src="https://cdn-icons-png.flaticon.com/128/16416/16416833.png" alt="" width="30" height="30">
     </div>
     <div class="w-full p-1" >
         <span class="text-slate-400 text-xs">Current Value</span>
        <p class="text-slate-700 text-xs"><span><i class="pi pi-indian-rupee " style="font-size: 12px;"></i></span> <span >{{ currentvalue }}</span></p>
     </div>
</div>
</div>
<div>

</div>
</li>


<li class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow">
<div class="flex w-full items-center justify-between space-x-6 p-2">
<div class="flex truncate">
<div class="flex justify-center items-center p-3 bg-green-50 rounded-full"  >
         <img src="https://cdn-icons-png.flaticon.com/128/5501/5501360.png" alt="" width="30" height="30">
     </div>                
     <div class="w-full p-1" >
         <span class="text-slate-400 text-xs">Overall Gain</span>
         <p  class="text-slate-700 text-xs"> <span><i class="pi pi-indian-rupee text-xs" style="font-size: 12px;"></i></span> <span >{{ overallgain }}</span></p>
     </div>
</div>
</div>
<div>

</div>
</li>

<li class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow">
<div class="flex w-full items-center justify-between space-x-6 p-2">
<div class="flex truncate">
<div class="flex justify-center items-center p-3 bg-green-50 rounded-full"  >
         <img src="https://cdn-icons-png.flaticon.com/128/5501/5501360.png" alt="" width="30" height="30">
     </div>              
      <div class="w-full p-1" >
         <span class="text-slate-400 text-xs">Today's Gain</span>
         <p  class="text-slate-700 text-xs"> <span><i class="pi pi-indian-rupee text-xs" style="font-size: 12px;"></i></span> <span >{{ todaygain }}</span></p>
      </div>

</div>
</div>
<div>

</div>
</li>

</ul>
    </div>
  </div>

  <div class="overflow-hidden rounded-lg bg-white  mt-1">
    <div class="px-1 py-2 ">
      <DataTable  ref="dt" v-model:filters="filters"  paginator :rows="10" showGridlines removableSort    filterDisplay="menu" :globalFilterFields="['stockname', 'quantity']" stripedRows :value="filteredCustomers"  >



<template #header>
      <div class="flex justify-end">
          <IconField  class="w-full">
              <InputIcon>
                  <i class="pi pi-search" />
              </InputIcon>
              <InputText v-model="filters['global'].value" placeholder="Search stock and company" class="w-full" />
          </IconField>
      </div>




  </template>



<Column   v-if="visibleColumns.includes('stockname')" sortable field="stockname" header="StockName" class="text-sm cursor-pointer">
  <template #body="{ data }">
          <span  @click="topcanva(data)">{{ data.stockname }}</span>
      </template>
      <template #filter="{ filterModel }">
          <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
      </template>
</Column>
<Column v-if="visibleColumns.includes('quantity')"  sortable field="quantity" header="Quantity" class="text-sm cursor-pointer" :showFilterOperator="false" :showFilterMatchModes="false" >
  <template #body="{ data }">
          <span  @click="topcanva(data)">{{ data.quantity }}</span>
      </template>
<template #filter="{ filterModel }">
  <Slider v-model="filterModel.value" range class="m-4" :min="1" :max="1000"></Slider>
  <div class="flex items-center justify-between px-2">
      <span>{{ filterModel.value ? filterModel.value[0] : 0 }}</span>
      <span>{{ filterModel.value ? filterModel.value[1] : 100 }}</span>
  </div>
</template>
</Column>








<Column class="cursor-pointer"   v-if="visibleColumns.includes('action')"  field="action" header="Action" :showFilterOperator="false" :showFilterMatchModes="false" >
  <template #body="{ data }">
 <button type="button"  @click="topcanva(data)" class="rounded-md   px-2 py-1.5 text-sm bg-indigo-600 font-semibold text-white shadow-sm " ><i class="pi pi-eye"></i></button>

 
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
            <span>{{ stockname }}</span>
          </div>
         </div>
         <div class="w-full p-1" >
          <hr>
          <Accordion value="0">
<AccordionPanel value="0">
    <AccordionHeader>Details</AccordionHeader>
    <AccordionContent>

      <div class="w-full  flex">
        <div class="w-full " ><span>Stock Name</span></div>
        <div class="w-full " ><span>{{stockname}}</span></div>
      </div>
      <div class="w-full  flex">
        <div class="w-full " ><span>Date</span></div>
        <div class="w-full " ><span>{{dateval}}</span></div>
      </div>
      <div class="w-full  flex">
        <div class="w-full " ><span>Quantity</span></div>
        <div class="w-full " ><span>{{quant}}</span></div>
      </div>
      <div class="w-full  flex">
        <div class="w-full " ><span>AVG Price</span></div>
        <div class="w-full " ><span>{{avg}}</span></div>
      </div>
      <div class="w-full  flex">
        <div class="w-full " ><span>LTP</span></div>
        <div class="w-full " ><span>{{ltp}}</span></div>
      </div>
      <div class="w-full  flex">
        <div class="w-full " ><span>INV Amount</span></div>
        <div class="w-full " ><span>{{invamt}}</span></div>
      </div>
      <div class="w-full  flex">
        <div class="w-full " ><span>MKT Value</span></div>
        <div class="w-full " ><span>{{mktval}}</span></div>
      </div>
      <div class="w-full  flex">
        <div class="w-full " ><span>Over All</span></div>
        <div class="w-full " ><span>{{overall}}</span></div>
      </div>
      <div class="w-full  flex">
        <div class="w-full " ><span>Days</span></div>
        <div class="w-full " ><span>{{days}}</span></div>
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
import { ref, onMounted } from 'vue';
import DatePicker from 'primevue/datepicker';
import { FilterMatchMode, FilterOperator } from '@primevue/core/api';
import { useToast } from "primevue/usetoast";


const loading=ref(true)
const content=ref(false)
const toast = useToast();

const investamount=ref('')
const currentvalue=ref('')
const overallgain=ref('')
const todaygain=ref('')




const filters = ref();

const customers = ref([]);
const start = ref(null);
const end = ref(null);
const filteredCustomers = ref([]);
const activeFilter = ref('week'); // Track active filter


const startdate=ref('')
const enddate=ref('')



const selectedTab = ref('activity');
const changeTab = (tab) => {
  selectedTab.value = tab;
};

const initFilters = () => {
  filters.value = {
      global: { value: null, matchMode: FilterMatchMode.CONTAINS },
      stockname: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
quantity: { value: [0, 100], matchMode: FilterMatchMode.BETWEEN },


  };
};



initFilters();
const getdata = async () => {
  try {
    const res = await fetch('/sharetable.json');
    if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
    customers.value = await res.json();
    filterLastWeek(); // Apply 7-day filter on page load
  } catch (error) {
    console.error('Error:', error.message);
  }
};

// Function to filter last 7 days
const filterLastWeek = async () => {
  setInterval(() => {
    loading.value = false;
    content.value = true;
  }, 1000);
  const today = new Date();
  try {
    const res = await fetch('/amounttable.json');
    if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
    const data = await res.json();
    investamount.value = data[0].week.investamount;
    currentvalue.value = data[0].week.currentvalue;
    overallgain.value = data[0].week.overallgain;
    todaygain.value = data[0].week.todaygain;
  } catch (error) {
    console.error("Error:", error.message);
  }
  today.setHours(23, 59, 59, 999);

  const sevenDaysAgo = new Date();
  sevenDaysAgo.setDate(today.getDate() - 6);
  sevenDaysAgo.setHours(0, 0, 0, 0);

  // Filter customers within the last week
  filteredCustomers.value = customers.value.filter(customer => {
    const customerDate = new Date(customer.date);
    return customerDate >= sevenDaysAgo && customerDate <= today;
  });

  activeFilter.value = 'week'; // Update active filter
 

  // Log first and last date if data exists
  if (filteredCustomers.value.length > 0) {
    const formatDate = (date) => {
      const d = new Date(date);
      const day = String(d.getDate()).padStart(2, '0');
      const month = String(d.getMonth() + 1).padStart(2, '0');
      const year = d.getFullYear();
      return `${day}-${month}-${year}`;
    };

    const stdate= filteredCustomers.value[0].date;
   const endate = filteredCustomers.value[filteredCustomers.value.length - 1].date;

    startdate.value = formatDate(stdate);
    enddate.value = formatDate(endate);

    start.value=startdate.value
    end.value=enddate.value

    console.log(start.value);
  } else {
    console.log("No customers found in the last week.");
  }

  visibleTop.value=false
};


// Function to filter last 15 days
const filterLast15Days = async() => {

  try {

const res = await fetch('/amounttable.json');
if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
const data = await res.json();
investamount.value=data[1].day_15.investamount
currentvalue.value=data[1].day_15.currentvalue
overallgain.value=data[1].day_15.overallgain
todaygain.value=data[1].day_15.todaygain

} catch (error) {
console.error("Error:", error.message);
}

  const today = new Date();
  const fifteenDaysAgo = new Date();
  fifteenDaysAgo.setDate(today.getDate() - 15);

  filteredCustomers.value = customers.value.filter(customer => {
    const customerDate = new Date(customer.date);
    return customerDate >= fifteenDaysAgo && customerDate <= today.setHours(23, 59, 59, 999);
  });

  if (filteredCustomers.value.length > 0) {
    const formatDate = (date) => {
      const d = new Date(date);
      const day = String(d.getDate()).padStart(2, '0');
      const month = String(d.getMonth() + 1).padStart(2, '0');
      const year = d.getFullYear();
      return `${day}-${month}-${year}`;
    };

   const stdate= filteredCustomers.value[0].date;
   const endate = filteredCustomers.value[filteredCustomers.value.length - 1].date;

    startdate.value = formatDate(stdate);
    enddate.value = formatDate(endate);

    start.value=startdate.value
    end.value=enddate.value
 
  } else {
    console.log("No customers found in the last week.");
  }
  activeFilter.value = '15days'; // Update active filter state
  console.log('Filtered last 15 days', filteredCustomers.value);
  visibleTop.value=false
};

// Function to filter last month
const filterLastMonth = async() => {

  try {

const res = await fetch('/amounttable.json');
if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
const data = await res.json();
investamount.value=data[2].month.investamount
currentvalue.value=data[2].month.currentvalue
overallgain.value=data[2].month.overallgain
todaygain.value=data[2].month.todaygain

} catch (error) {
console.error("Error:", error.message);
}

  const today = new Date();
  const lastMonth = new Date();
  lastMonth.setMonth(today.getMonth() - 1);

  filteredCustomers.value = customers.value.filter(customer => {
    const customerDate = new Date(customer.date);
    return customerDate >= lastMonth && customerDate <= today.setHours(23, 59, 59, 999);
  });

  if (filteredCustomers.value.length > 0) {
    const formatDate = (date) => {
      const d = new Date(date);
      const day = String(d.getDate()).padStart(2, '0');
      const month = String(d.getMonth() + 1).padStart(2, '0');
      const year = d.getFullYear();
      return `${day}-${month}-${year}`;
    };

    const stdate= filteredCustomers.value[0].date;
   const endate = filteredCustomers.value[filteredCustomers.value.length - 1].date;

    startdate.value = formatDate(stdate);
    enddate.value = formatDate(endate);

    start.value=startdate.value
    end.value=enddate.value

   
  } else {
    console.log("No customers found in the last week.");
  }
  activeFilter.value = 'month'; // Update active filter state
  console.log('Filtered last month', filteredCustomers.value);
  visibleTop.value=false
};

// Function to filter last 3 months
const filterLast3Months = async() => {

  try {

const res = await fetch('/amounttable.json');
if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
const data = await res.json();
investamount.value=data[3].month_3.investamount
currentvalue.value=data[3].month_3.currentvalue
overallgain.value=data[3].month_3.overallgain
todaygain.value=data[3].month_3.todaygain

} catch (error) {
console.error("Error:", error.message);
}

  const today = new Date();
  const threeMonthsAgo = new Date();
  threeMonthsAgo.setMonth(today.getMonth() - 3);

  filteredCustomers.value = customers.value.filter(customer => {
    const customerDate = new Date(customer.date);
    return customerDate >= threeMonthsAgo && customerDate <= today.setHours(23, 59, 59, 999);
  });

  if (filteredCustomers.value.length > 0) {
    const formatDate = (date) => {
      const d = new Date(date);
      const day = String(d.getDate()).padStart(2, '0');
      const month = String(d.getMonth() + 1).padStart(2, '0');
      const year = d.getFullYear();
      return `${day}-${month}-${year}`;
    };

    const stdate= filteredCustomers.value[0].date;
   const endate = filteredCustomers.value[filteredCustomers.value.length - 1].date;

    startdate.value = formatDate(stdate);
    enddate.value = formatDate(endate);

    start.value=startdate.value
    end.value=enddate.value

  } else {
    console.log("No customers found in the last week.");
  }

  activeFilter.value = '3months'; // Update active filter state
  console.log('Filtered last 3 months', filteredCustomers.value);
  visibleTop.value=false
};

const applyFilter = () => {
  if (!start.value || !end.value) {
    filteredCustomers.value = customers.value;
    return;
  }

  // Convert date values to dd-mm-yyyy format
  const startDate = new Date(start.value);
  const endDate = new Date(end.value);
  
  const formatDate = (date) => {
    return `${String(date.getDate()).padStart(2, '0')}-${String(date.getMonth() + 1).padStart(2, '0')}-${date.getFullYear()}`;
  };

  startdate.value=formatDate(startDate)
  enddate.value=formatDate(endDate)


  filteredCustomers.value = customers.value.filter(customer => {
    const customerDate = new Date(customer.date);
    return customerDate >= startDate && customerDate <= endDate.setHours(23, 59, 59, 999);
  });

  activeFilter.value = ''; // Reset filter state when custom date is selected
  visibleTop.value = false;
};


onMounted(() => {
  getdata();
});
const visibleTop=ref(false)
const customtoggle = () => {

 visibleTop.value = true
};

const columns = ref([
{ field: 'stockname', header: 'Stockname' },
{ field: 'quantity', header: 'Quantity' },
{ field: 'action', header: 'Action' },
]);
//Initially select all columns except 'ltp', 'mktval', and 'date'
const selectedColumns = ref(columns.value.filter(col => !['ltp', 'mktval', 'date'].includes(col.field)));
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

const visibleTop2=ref(false)
const stockname=ref('')
const dateval=ref('')
const quant=ref('')
const avg=ref('')
const ltp=ref('')
const invamt=ref('')
const mktval=ref('')
const overall=ref('')
const days=ref('')

const topcanva =(dataval)=>{
  visibleTop2.value=true

stockname.value=dataval.stockname
dateval.value=dataval.date
quant.value=dataval.quantity
avg.value=dataval.avgprice
ltp.value=dataval.ltp
invamt.value=dataval.invamt
mktval.value=dataval.mktval
overall.value=dataval.overall
days.value=dataval.days
}

const proceedfun=async()=>{
const formdata=new FormData()
formdata.append('stockname', stockname.value)
formdata.append('date', dateval.value)
formdata.append('quantity', quant.value)
formdata.append('averageprice', avg.value)
formdata.append('ltp', ltp.value)
formdata.append('invamt', invamt.value)
formdata.append('mktval', mktval.value)
formdata.append('overall', overall.value)
formdata.append('days', days.value)
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
formdata.append('stockname', stockname.value)
formdata.append('date', dateval.value)
formdata.append('quantity', quant.value)
formdata.append('averageprice', avg.value)
formdata.append('ltp', ltp.value)
formdata.append('invamt', invamt.value)
formdata.append('mktval', mktval.value)
formdata.append('overall', overall.value)
formdata.append('days', days.value)
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
<style>

.p-paginator .p-paginator-pages .p-paginator-page {
  background-color: #5fa5f5 !important; 
    color: white !important; 
   
   
}


.p-paginator .p-paginator-pages .p-paginator-page:hover {
    background-color: #0056b3 !important;
}


</style>