<template>

  <div class="flex justify-center items-center w-screen h-screen overflow-hidden">
    <div class="rounded-xl bg-white flex gap-10 p-4 m-3 absolute shadow-lg">
      <div class="rounded-xl relative">
        <img src="/images/bg-sidebar-desktop.svg" alt="side bar desktop" class="w-[18.9rem] lg:block hidden">
        <div class="absolute top-10 left-10 flex flex-col gap-7">
          <Step :stepCount="1" description="your info" :isActive="currentStep === 1" />
          <Step :stepCount="2" description="Select plan" :isActive="currentStep === 2" />
          <Step :stepCount="3" description="Add-ons" :isActive="currentStep === 3" />
          <Step :stepCount="4" description="Summary" :isActive="currentStep >= 4 " />
        </div>
      </div>

      <!-- First Step -->

      <div class="w-[42rem] px-20">
        <div class="flex flex-col h-full" v-if="currentStep === 1">
          <div class="mt-10">
            <StepDesc title="Personal info" subtitle="Please provide your name, email address, and phone number." />
            <div class="flex flex-col gap-3 mt-8">
              <Input 
                name="Name" 
                placeholder="e.g. Stephen King" 
                type="text" 
                v-model="formData.name" 
                :error="errors.name" 
                :required="true"
              />
              <Input 
                name="Email address" 
                placeholder="e.g. stephenking@lorem.com" 
                type="email" 
                v-model="formData.email" 
                :error="errors.email" 
                :required="true"
              />
              <Input 
                name="Phone Number" 
                placeholder="e.g. +1 234 567 890" 
                type="text" 
                v-model="formData.phoneNumber" 
                :error="errors.phoneNumber"
                :required="true" 
              />
            </div>
          </div>
          <div class="self-end mt-auto mb-5">
            <Button @nextStep="nextStep">Next Step</Button>
          </div>
        </div>

        <div class="flex flex-col h-full" v-else-if="currentStep === 2">
          <div class="mt-10">
            <StepDesc title="Select your plan" subtitle="You have the option of monthly or yearly earning billing." />
            <div class="flex gap-5 mt-8 min-h-48">
              <Plan 
                :iconLink="'/images/icon-arcade.svg'"
                :name="'Arcade'"
                :billing="billing"
                :price="9"
                :isActive="planSelected.name === 'Arcade'"
                @changePlan="changePlan"
                :montlyOrYearly="montlyOrYearly"

              />
              <Plan 
                :iconLink="'/images/icon-advanced.svg'"
                :name="'Advanced'"
                :billing="billing"
                :price="12"
                :isActive="planSelected.name === 'Advanced'"
                @changePlan="changePlan"
                :montlyOrYearly="montlyOrYearly"

              />
              <Plan 
                :iconLink="'/images/icon-pro.svg'"
                :name="'Pro'"
                :billing="billing"
                :price="15"
                :isActive="planSelected.name === 'Pro'"
                @changePlan="changePlan"
                :montlyOrYearly="montlyOrYearly"

              />
            </div>
            <div class="flex gap-7 items-center justify-center bg-magnolia py-4 mt-8 rounded-md">
              <p :class="`font-bold ${billing === 'monthly' ? 'text-marine-blue' : 'text-cool-gray'}`">Monthly</p>
              <button @click="changeBilling" class="w-10 h-5 bg-marine-blue rounded-xl p-1 flex items-center relative">
                <div :class="`w-3 h-3 rounded-full bg-white absolute ${billing === 'monthly' ? 'left-1' : 'translate-x-5'} transition duration-50 ease-out`"></div>
              </button>
              <p :class="`font-bold ${billing === 'yearly' ? 'text-marine-blue' : 'text-cool-gray'}`">Yearly</p>
            </div>
          </div>
          <div class="flex justify-between mt-auto mb-5">
            <GoBackButton @previousStep="previousStep" />
            <Button @nextStep="nextStep">Next Step</Button>
          </div>
        </div>
        
        <div class="flex flex-col h-full" v-else-if="currentStep === 3">
          <div class="mt-10">
            <StepDesc title="Pick Add-ons" subtitle="Add-ons help enhance your gaming experience." />
            <div class="flex flex-col gap-5 mt-8">
              <AddOns 
                :title="'Online service'"
                :subtitle="'Access to multiplayer games'"
                :billing="billing"
                :price="1"
                :isActive="isOnlineServiceSelected"
                @changeSelectionExtra="() => isOnlineServiceSelected = !isOnlineServiceSelected"
                :montlyOrYearly="montlyOrYearly"
              />
              <AddOns 
                :title="'Larger storage'"
                :subtitle="'Extra 1TB of cloud save'"
                :billing="billing"
                :price="2"
                :isActive="isLargerStorageSelected"
                @changeSelectionExtra="() => isLargerStorageSelected = !isLargerStorageSelected"
                :montlyOrYearly="montlyOrYearly"
              />
              <AddOns 
                :title="'Customizable profile'"
                :subtitle="'Custom theme on your profile'"
                :billing="billing"
                :price="2"
                :isActive="isCustomProfileSelected"
                @changeSelectionExtra="() => isCustomProfileSelected = !isCustomProfileSelected"
                :montlyOrYearly="montlyOrYearly"
              />
            </div>
          </div>
          <div class="flex justify-between mt-auto mb-5">
            <GoBackButton @previousStep="previousStep" />
            <Button @nextStep="nextStep">Next Step</Button>
          </div>
        </div>

        <div class="flex flex-col h-full" v-else-if="currentStep === 4">
          <div class="mt-10">
            <StepDesc title="Finishing up" subtitle="Double check everything looks OK before confirming." />
            <div class="px-7 py-5 bg-magnolia rounded-xl mt-8">
              <div class="flex justify-between items-center">
                <div class="flex flex-col">
                  <span class="text-marine-blue font-bold">{{ planSelected.name }} {{ billing === 'monthly' ? '(Monthly)' : '(Yearly)' }}</span>
                  <button @click="() => currentStep = 2" class="text-cool-gray underline hover:text-purplish-blue transition duration-200 text-left">Change</button>
                </div>
                <span class="font-bold text-marine-blue">{{ montlyOrYearly(planSelected.price) }}</span>
              </div>
              <hr class="my-5">
              <div class="flex flex-col gap-5">
                <div class="flex justify-between items-center" v-if="isOnlineServiceSelected">
                  <span class="text-cool-gray">Online Service</span>
                  <span class="text-marine-blue">+{{ montlyOrYearly(1) }}</span>
                </div>
                <div class="flex justify-between items-center"  v-if="isLargerStorageSelected">
                  <span class="text-cool-gray">Larger storage</span>
                  <span class="text-marine-blue">+{{ montlyOrYearly(2) }}</span>
                </div>
                <div class="flex justify-between items-center"  v-if="isCustomProfileSelected">
                  <span class="text-cool-gray">Customizable profile</span>
                  <span class="text-marine-blue">+{{ montlyOrYearly(2) }}</span>
                </div>
              </div>
            </div>
          </div>
          <div class="mt-5 flex justify-between items-center">
            <span class="text-cool-gray">Total {{ billing === 'monthly' ? '(per month)' : '(per year)' }}</span>
            <span class="text-purplish-blue font-bold text-xl">+${{ billing === 'monthly' ? totalPrice + '/mo' : totalPrice + '/yr' }}</span>
          </div>
          <div class="flex justify-between mt-auto mb-5">
            <GoBackButton @previousStep="previousStep" />
            <Button @nextStep="nextStep" :customColor="'bg-purplish-blue'" :customHover="'hover:opacity-80'">Confirm</Button>
          </div>
        </div>
        <div class="h-full flex flex-col justify-center gap-7 text-center items-center" v-else-if="currentStep === 5">
          <img src="/images/icon-thank-you.svg" alt="Thank you icon">
          <StepDesc title="Thank you!" subtitle="Thanks for confirming your subscription! We hope you have fun using our platform. If you ever need support, please feel free to email us at support@loremgaming.fr." /> 
        </div>
      </div>
    </div>
  </div>


</template>


<script setup>

import Step from './components/Step.vue';
import { computed, ref } from 'vue';
import StepDesc from './components/StepDesc.vue';
import Input from './components/Input.vue';
import Button from './components/Button.vue';
import Plan from './components/Plan.vue';
import GoBackButton from './components/GoBackButton.vue';
import AddOns from './components/AddOns.vue';

const currentStep = ref(2);
const currency = '$';

const montlyOrYearly = (price) => {
  if (billing === 'monhtly') {
    return currency + price + '/mo'
  } else {
    return currency + price * 10 + '/yo'
  }
}

function nextStep(){

  if(currentStep.value === 1 && !isFirstStepValid()) return;

  currentStep.value++;
}

function previousStep(){
  currentStep.value--;  
}


// First Step

const errors = ref({
  name: '',
  email: '',
  phoneNumber: ''
})

const formData = ref({
  name: '',
  email: '',
  phoneNumber: ''
})

const isValidName = () => formData.value.name !== '';
const isValidEmail = () => formData.value.email !== '' && formData.value.email.match(/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/);
const isValidPhoneNumber = () => formData.value.phoneNumber !== '' && formData.value.phoneNumber.match(/^\d+$/);

function isFirstStepValid(){
  let valid = true;
  if(!isValidName()) {
    errors.value.name = "Please put a valid name.";
    valid = false;
  } else {
    errors.value.name = "";
  }

  if(!isValidEmail()) {
    errors.value.email = "Please put a valid email.";
    valid = false;
  } else {
    errors.value.email = "";
  }

  if(!isValidPhoneNumber()) {
    errors.value.phoneNumber = "Please put a valid number.";
    valid = false;
  } else {
    errors.value.phoneNumber = "";
  }

  return valid;
}

// Second Step


const billing = ref('monthly');
const planSelected = ref({name: 'Arcade', price: 9});

function changePlan(plan){
  planSelected.value = plan;
}

function changeBilling(){
  billing.value = billing.value === 'monthly' ? 'yearly' : 'monthly';
}


// Third Step

const isOnlineServiceSelected = ref(false);
const isLargerStorageSelected = ref(false);
const isCustomProfileSelected = ref(false);

// Summary

const totalPrice = computed(() => {
  let totalPrice = 0;
  totalPrice += billing.value === 'monthly' ? planSelected.value.price : planSelected.value.price * 10; 
  if(isOnlineServiceSelected.value) totalPrice += billing.value === 'monthly' ? 1 : 10;
  if(isLargerStorageSelected.value) totalPrice += billing.value === 'monthly' ? 2 : 20;
  if(isCustomProfileSelected.value) totalPrice += billing.value === 'monthly' ? 2 : 20;
  return totalPrice;
})


</script>