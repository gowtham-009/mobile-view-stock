<template>

    <Toast />
       
    <div class="overflow-hidden rounded-lg bg-white ">
    <div class="px-1 py-1 ">
      <div class=" flex justify-between  gap-2  text-lg" >
       
       <div class="w-full flex gap-2" >
        <div>
          <div class="w-full text-black-400 text-md" > Statement For</div>
        <div class="w-full text-indigo-500 " style=" margin-top: -8px; font-size:10px;"> {{ startdate }} To {{ enddate }}</div>
        </div>

        <div class="w-4 h4">
          <button type="button"   @click="customtoggle()"  class="rounded-md  px-1 py-1 text-sm font-semibold text-slate-500   border-2">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
                <path fill-rule="evenodd" d="M6.75 2.25A.75.75 0 0 1 7.5 3v1.5h9V3A.75.75 0 0 1 18 3v1.5h.75a3 3 0 0 1 3 3v11.25a3 3 0 0 1-3 3H5.25a3 3 0 0 1-3-3V7.5a3 3 0 0 1 3-3H6V3a.75.75 0 0 1 .75-.75Zm13.5 9a1.5 1.5 0 0 0-1.5-1.5H5.25a1.5 1.5 0 0 0-1.5 1.5v7.5a1.5 1.5 0 0 0 1.5 1.5h13.5a1.5 1.5 0 0 0 1.5-1.5v-7.5Z" clip-rule="evenodd" />
                </svg>
            </button>

        </div>
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
  
    <div  class="w-full" v-if="loading">
      <div class="p-1 space-y-4">
    
      <dl class="mx-auto grid grid-cols-2 gap-px bg-gray-900/5">
    <div class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-2 bg-white px-4 py-10 sm:px-6 xl:px-8 animate-pulse">
      <dt class="h-4 w-20 bg-gray-300 rounded"></dt>
      <dd class="h-3 w-10 bg-gray-300 rounded"></dd>
      <dd class="w-full h-8 bg-gray-300 rounded"></dd>
    </div>
    <div class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-2 bg-white px-4 py-10 sm:px-6 xl:px-8 animate-pulse">
      <dt class="h-4 w-20 bg-gray-300 rounded"></dt>
      <dd class="h-3 w-10 bg-gray-300 rounded"></dd>
      <dd class="w-full h-8 bg-gray-300 rounded"></dd>
    </div>
    <div class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-2 bg-white px-4 py-10 sm:px-6 xl:px-8 animate-pulse">
      <dt class="h-4 w-20 bg-gray-300 rounded"></dt>
      <dd class="h-3 w-10 bg-gray-300 rounded"></dd>
      <dd class="w-full h-8 bg-gray-300 rounded"></dd>
    </div>
    <div class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-2 bg-white px-4 py-10 sm:px-6 xl:px-8 animate-pulse">
      <dt class="h-4 w-20 bg-gray-300 rounded"></dt>
      <dd class="h-3 w-10 bg-gray-300 rounded"></dd>
      <dd class="w-full h-8 bg-gray-300 rounded"></dd>
    </div>
  </dl>
  
   
    
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
  
  
  
  <div class="w-full" v-if="content">
  <div class="overflow-hidden rounded-lg bg-white shadow  mt-1">
      <div class="px-2 py-2 ">
  
   <dl class="mx-auto grid grid-cols-2 gap-px bg-gray-900/5 ">
    <div class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-2  bg-white px-4 py-10 sm:px-6 xl:px-8">
      <dt class="text-sm/6 font-medium text-gray-500">Invested Amount</dt>
      <dd class="text-xs font-medium text-gray-700">+4.75%</dd>
      <dd class="w-full flex-none text-3xl/10 font-medium tracking-tight  text-gray-900">₹{{ investamount }}</dd>
    </div>
    <div class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-2 bg-white px-4 py-10 sm:px-6 xl:px-8">
      <dt class="text-sm/6 font-medium text-gray-500">Current Value</dt>
      <dd class="text-xs font-medium text-rose-600">+54.02%</dd>
      <dd class="w-full flex-none text-3xl/10 font-medium tracking-tight text-gray-900">₹{{ currentvalue }}</dd>
    </div>
    <div class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-2 bg-white px-4 py-10 sm:px-6 xl:px-8">
      <dt class="text-sm/6 font-medium text-gray-500">Overall Gain</dt>
      <dd class="text-xs font-medium text-gray-700">-1.39%</dd>
      <dd class="w-full flex-none text-3xl/10 font-medium tracking-tight text-gray-900">₹{{ overallgain }}</dd>
    </div>
    <div class="flex flex-wrap items-baseline justify-between gap-x-4 gap-y-2 bg-white px-4 py-10 sm:px-6 xl:px-8">
      <dt class="text-sm/6 font-medium text-gray-500">Today's Gain</dt>
      <dd class="text-xs font-medium text-rose-600">+10.18%</dd>
      <dd class="w-full flex-none text-3xl/10 font-medium tracking-tight text-gray-900">₹{{ todaygain }}</dd>
    </div>
  </dl>   
      </div>
    </div>
  
    <div class="overflow-hidden rounded-lg bg-white  mt-2">
      <div class="p-1 py-2 ">
        <DataTable  ref="dt" v-model:filters="filters" paginator :rows="10" removableSort :loading="loading" filterDisplay="menu" :globalFilterFields="['scriptname', 'orderid', 'date']" stripedRows :value="filteredCustomers"  >
  
  
  
  <template #header>
        <div class="flex justify-end items-center">
            <IconField >
                <InputIcon>
                    <i class="pi pi-search mb-2" />
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
  
  <Column  class="cursor-pointer"  v-if="visibleColumns.includes('scriptname')" sortable field="scriptname" header="Script Name">
    <template #body="{ data }">
           <span @click="topcanva(data)"> {{ data.scriptname }}</span>
        </template>
        <template #filter="{ filterModel }">
            <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
        </template>
  </Column>
  <Column  class="cursor-pointer" v-if="visibleColumns.includes('orderid')"  sortable field="orderid" header="OrderID" :showFilterOperator="false" :showFilterMatchModes="false">
    <template #body="{ data }">
           <span @click="topcanva(data)"> {{ data.orderid }}</span>
        </template>
        <template #filter="{ filterModel }">
            <InputText v-model="filterModel.value" type="text" placeholder="Search by name" />
        </template>
  </Column>
 
  
  
 
  
  

 
 
  <Column  class="cursor-pointer" v-if="visibleColumns.includes('date')" field="date" dataType="date" sortable header="Date" :showFilterOperator="false" :showFilterMatchModes="false">
    <template #body="{ data }">
  <span @click="topcanva(data)">{{ formatDatee(data.date) }}</span>
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
          <span>{{ scriptname }}</span>
        </div>
       </div>
       <div class="w-full mt-2">
        
        <Accordion value="0">
    <AccordionPanel value="0">
        <AccordionHeader>Details</AccordionHeader>
        <AccordionContent>
    
          <div class="w-full  flex">
            <div class="w-full " ><span>Script Name</span></div>
            <div class="w-full " ><span>{{scriptname}}</span></div>
          </div>
          <div class="w-full  flex">
            <div class="w-full " ><span>Order ID</span></div>
            <div class="w-full " ><span>{{orderid}}</span></div>
          </div>
          <div class="w-full  flex">
            <div class="w-full " ><span>Date</span></div>
            <div class="w-full " ><span>{{date}}</span></div>
          </div>
          <div class="w-full  flex">
            <div class="w-full " ><span>Action</span></div>
            <div class="w-full " ><span>{{action}}</span></div>
          </div>
          <div class="w-full  flex">
            <div class="w-full " ><span>Quantity</span></div>
            <div class="w-full " ><span>{{quantity}}</span></div>
          </div>
          <div class="w-full  flex">
            <div class="w-full " ><span>Buy Sell Price</span></div>
            <div class="w-full " ><span>{{buysell}}</span></div>
          </div>
          <div class="w-full  flex">
            <div class="w-full " ><span>Brockage</span></div>
            <div class="w-full " ><span>{{brockage}}</span></div>
          </div>
          <div class="w-full  flex">
            <div class="w-full " ><span>charges</span></div>
            <div class="w-full " ><span>{{charges}}</span></div>
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
  import 'primeicons/primeicons.css'

  const selectedTab = ref('activity');
const changeTab = (tab) => {
  selectedTab.value = tab;
};


  const formatDatee = (dateString) => {
    if (!dateString) return "";
    const [year, month, day] = dateString.split("-");
    return `${day}-${month}-${year.slice(-4)}`; // Convert yy-mm-dd to dd-mm-yy
  };
  
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
  
  const initFilters = () => {
    filters.value = {
        global: { value: null, matchMode: FilterMatchMode.CONTAINS },
        scriptname: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        orderid: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
        date: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.EQUALS }] },
        
     };
  };
  

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
  
  initFilters();
  const getdata = async () => {
    try {
      const res = await fetch('/trades.json');
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
      customers.value = await res.json();
      filterLastWeek(); // Apply 7-day filter on page load
    } catch (error) {
      console.error('Error:', error.message);
    }
  };
  

  const visibleTop=ref(false)
const customtoggle = () => {

 visibleTop.value = true
};

  // Function to filter last 7 days
  const filterLastWeek = async () => {
   
    setInterval(() => {
      loading.value=false
      content.value=true
    }, 1000);
    const today = new Date();
    try {
  
  const res = await fetch('/amounttable.json');
  if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`);
  const data = await res.json();
  investamount.value=data[0].week.investamount
  currentvalue.value=data[0].week.currentvalue
  overallgain.value=data[0].week.overallgain
  todaygain.value=data[0].week.todaygain
  
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
  
      console.log(start.value);
    } else {
      console.log("No customers found in the last week.");
    }
  
    activeFilter.value = '3months'; 
  
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
  
  };
  
  onMounted(() => {
    getdata();
  });
  
  
  
  const columns = ref([
  { field: 'scriptname', header: 'Scriptname' },
  { field: 'orderid', header: 'Orderid' },
  { field: 'date', header: 'Date' },

 
  
  ]);
  //Initially select all columns except 'ltp', 'mktval', and 'date'
  const selectedColumns = ref(columns.value.filter(col => !['date'].includes(col.field)));
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
  const scriptname=ref('')
  const orderid=ref('')
  const date=ref('')
  const action=ref('')
  const quantity=ref('')
  const buysell=ref('')
  const brockage=ref('')
  const charges=ref('')
  

  

  
const topcanva =(dataval)=>{
  visibleTop2.value=true

  scriptname.value=dataval.scriptname
  orderid.value=dataval.orderid
  date.value=dataval.date
  action.value=dataval.action
  quantity.value=dataval.quantity
  buysell.value=dataval.buysellprice
  brockage.value=dataval.brokerage
  charges.value=dataval.charges
}

  const proceedfun=async()=>{
  const formdata=new FormData()
  formdata.append('scriptname',  scriptname.value)
  formdata.append('orderid',  orderid.value)
  formdata.append('date', date.value)
  formdata.append('action', action.value)
  formdata.append('quant', quantity.value)
  formdata.append('buysell', buysell.value)
  formdata.append('brockage', brockage.value)
  formdata.append('charges',charges.value)
  
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
  formdata.append('scriptname',  scriptname.value)
  formdata.append('orderid',  orderid.value)
  formdata.append('date', date.value)
  formdata.append('action', action.value)
  formdata.append('quant', quantity.value)
  formdata.append('buysell', buysell.value)
  formdata.append('brockage', brockage.value)
  formdata.append('charges',charges.value)
  
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
  
  .p-checkbox-checked.p-variant-filled .p-checkbox-box{
    background-color: blue !important;
    border: blue !important;
  }
 
  .p-multiselect.p-variant-filled{
    background: none !important;
  }
  .p-multiselect{
    border: none !important;
    box-shadow: none !important;
  }
  .p-multiselect-dropdown{
    border: 2px solid rgb(227, 227, 227);
    border-radius: 5px;
  }
  </style>