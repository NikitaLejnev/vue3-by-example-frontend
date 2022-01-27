<template>
  <Card v-for="c of catalog" :key="c.id">
    <template #header>
      <img :alt="c.description" :src="c.image_url" />
    </template>
    <template #title>{{ c.name }}</template>
    <template #content>{{ c.description }}</template>
    <template #footer>
      <Button icon="pi pi-check" label="Book" class="p-button-secondary" @click="book(c.id)" />
      <Dialog header="Create Booking" v-model:visible="displayBookingForm">
        <BookingForm
          @booking-form-close="displayBookingForm = false; displayMessage(); "
          :selectedCatalogId="selectedCatalogId"
        />
      </Dialog>
    </template>
  </Card>
</template>
