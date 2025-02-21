<template>
    <Dialog 
        :visible="modelValue" 
        @update:visible="$emit('update:modelValue', $event)"
        modal 
        header="Add Speaker" 
        :style="{ width: '50vw' }"
        class="p-fluid"
    >
        <div class="flex flex-col gap-4">
            <div class="field">
                <label for="location">Location</label>
                <AutoComplete
                    v-model="selectedLocation"
                    :suggestions="locationSuggestions"
                    @complete="searchLocation"
                    placeholder="Search for location..."
                    class="w-full"
                />
            </div>

            <div class="field">
                <label for="painting">Painting</label>
                <AutoComplete
                    v-model="selectedPainting"
                    :suggestions="paintingSuggestions"
                    @complete="searchPainting"
                    placeholder="Search for painting..."
                    class="w-full"
                />
            </div>

            <div class="field">
                <label for="language">Language</label>
                <Select
                    v-model="selectedLanguage"
                    :options="languages"
                    optionLabel="name"
                    placeholder="Select a language"
                    class="w-full"
                />
            </div>
        </div>

        <template #footer>
            <div class="flex justify-end gap-2">
                <Button label="Cancel" @click="closeDialog" text />
                <Button label="Save" @click="saveSpeaker" severity="primary" />
            </div>
        </template>
    </Dialog>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// Props and Emits
const props = defineProps<{
    modelValue: boolean
}>();

const emit = defineEmits<{
    'update:modelValue': [value: boolean]
}>();

// Form fields
const selectedLocation = ref('');
const selectedPainting = ref('');
const selectedLanguage = ref(null);

// Suggestions
const locationSuggestions = ref<string[]>([]);
const paintingSuggestions = ref<string[]>([]);

// Language options
const languages = ref([
    { name: 'English', code: 'en' },
    { name: 'Indonesian', code: 'id' },
    { name: 'Italian', code: 'it' }
]);

// AutoComplete search handlers
const searchLocation = (event: { query: string }) => {
    locationSuggestions.value = [
        'Floor 1 - Area A',
        'Floor 1 - Area B',
        'Floor 2 - Area A',
        'Floor 2 - Area B',
        'Floor 2 - Area C'
    ].filter(location => 
        location.toLowerCase().includes(event.query.toLowerCase())
    );
};

const searchPainting = (event: { query: string }) => {
    paintingSuggestions.value = [
        'The Last Supper',
        'The Creation of Adam',
        'Mona Lisa',
        'The Starry Night',
        'Guernica'
    ].filter(painting => 
        painting.toLowerCase().includes(event.query.toLowerCase())
    );
};

// Dialog handlers
const closeDialog = () => {
    emit('update:modelValue', false);
    resetForm();
};

const saveSpeaker = () => {
    // Add your save logic here
    console.log({
        location: selectedLocation.value,
        painting: selectedPainting.value,
        language: selectedLanguage.value
    });
    closeDialog();
};

const resetForm = () => {
    selectedLocation.value = '';
    selectedPainting.value = '';
    selectedLanguage.value = null;
};
</script>