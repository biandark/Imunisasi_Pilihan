<template>
    <app-layout>
        <template #header>
            <h2 class="font-bold text-xl text-center text-gray-800 leading-tight">
                Data Anggota Keluarga
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="p-6 max-w-4xl mx-auto">
                        <h3 class="font-semibold mt-6 text-xl text-indigo-500 leading-tight">
                                Daftar Anggota Keluarga
                        </h3>
                        <div class="mt-4 overflow-x-auto">
                            <table class="min-w-full leading-normal">
                                <thead>
                                    <tr>
                                        <th class="px-3 py-3">No</th>
                                        <th class="px-2 py-3">Nama</th>
                                        <th class="px-2 py-3">Tanggal Lahir</th>
                                        <th class="px-2 py-3">Jenis Kelamin</th>
                                        <th ></th>
                                        <th ></th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y text-sm">
                                    <tr v-for="(baby, index) in babies" :key="baby.id">
                                        <td class="px-2 py-1 text-center">{{ index+1 }}</td>
                                        <td class="px-2 py-1">{{ baby.nama }}</td>
                                        <td class="px-2 py-1 text-center">{{ formatDate(baby.ttl) }}</td>
                                        <td class="px-2 py-1 text-center">{{ baby.gender }}</td>
                                        <td class="text-right">
                                            <inertia-link v-if="checkAge(baby.ttl)" :href="route('form', {baby_id: baby.id})">
                                                <button class="border border-gray-200 bg-gray-200 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-gray-300 focus:outline-none focus:shadow-outline">
                                                    Imunisasi Wajib
                                                </button>
                                            </inertia-link>
                                            <inertia-link :href="route('kondisi', {baby_id: baby.id})">
                                                <button class="border border-gray-200 bg-gray-200 text-gray-700 rounded-md px-4 py-2 m-2 transition duration-500 ease select-none hover:bg-gray-300 focus:outline-none focus:shadow-outline">
                                                    Imunisasi Pilihan
                                                </button>
                                            </inertia-link>
                                        </td>
                                        <td>
                                            <inertia-link class="text-indigo-500" :href="route('riwayat', {baby_id:baby.id})">
                                                <div class="items-center text-sm font-semibold text-indigo-700">
                                                    <div>Riwayat Imunisasi Pilihan</div>
                                                </div>
                                            </inertia-link>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                            <div class="flex justify-center py-5">
                                <inertia-link :href="route('databayi.create')">
                                    <jet-button class="bg-indigo-500">
                                        Tambah Data Anak
                                    </jet-button>
                                </inertia-link>
                                <inertia-link :href="route('datakeluarga.create')">
                                    <jet-button class="bg-indigo-500 ml-5">
                                        Tambah Data Keluarga Lainnya
                                    </jet-button>
                                </inertia-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout'
    import Welcome from '@/Jetstream/Welcome'
    import JetButton from '@/Jetstream/Button'
    import { format, differenceInMonths } from 'date-fns'
    import { id } from 'date-fns/locale'

    export default {
        components: {
            AppLayout,
            Welcome,
            JetButton,
        },
        props: ['babies'],
        methods: {
            formatDate(date) {
                const tgl = new Date(date)
                return format(tgl, "d MMMM yyyy", {
                        locale: id
                    })
            },
            checkAge(ttl) {
                const ageInMonths = differenceInMonths(new Date(), new Date(ttl))
                return ageInMonths < 24
            } 
        },
    }
</script>