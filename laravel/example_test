
Ir al contenido
Uso de Gmail con lectores de pantalla
Meet
Chat
1 de 10.612
test
Recibidos
	x
Hector I. Depablos T.
	
21:10 (hace 56 minutos)
	
para mí
<?php

namespace Tests\Feature;

use Tests\TestCase;

class BankSellerCollectorTest extends TestCase
{
    public function testSellerCollectorList()
    {
        $this->seedData();
        $response = $this->post('/api/admin/bank-seller-collector', []);
        $response->assertStatus(200);
    }

    public function testSellerCollectorDataConfig()
    {
        $this->seedData();
        $response = $this->post('/api/admin/bank-seller-collector/data-config', []);
        $response->assertJsonStructure([
            'banks' => [['id', 'entity_code', 'name']], 'companies' => [['id', 'name']]
        ]);
        $response->assertStatus(200);
    }

    public function testSellerCollectorCreateBankIdRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["bank_id" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/create', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['bank_id']
            ]);
    }

    public function testSellerCollectorCreateSellerIdRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["seller_id" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/create', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['seller_id']
            ]);
    }

    public function testSellerCollectorCreateCollectorIdRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["collector_id" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/create', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['collector_id']
            ]);
    }

    public function testSellerCollectorCreateDebitDayRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["debit_day" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/create', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['debit_day']
            ]);
    }

    public function testSellerCollectorCreateWithBankIdExistRejected()
    {
        $this->seedData();
        $data = array_merge($this->rowSellerCollector(), ["bank_id" => 3]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/create', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['bank_id']
            ]);
    }

    public function testSellerCollectorCreate()
    {
        $response = $this->call('POST', '/api/admin/bank-seller-collector/create', $this->rowSellerCollector());

        $response->assertStatus(201);
        $this->assertDatabaseHas('bank_seller_collector', [
            'bank_id' => 2,
            'seller_id' => 2,
            'collector_id' => 4,
            'close_sales_month_day' => null,
            'debit_day' => 6
        ]);
    }

    public function testSellerCollectorUpdateIdRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["id" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/update', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['id']
            ]);
    }


    public function testSellerCollectorUpdateBankIdRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["bank_id" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/update', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['bank_id']
            ]);
    }

    public function testSellerCollectorUpdateSellerIdRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["seller_id" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/update', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['seller_id']
            ]);
    }

    public function testSellerCollectorUpdateCollectorIdRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["collector_id" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/update', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['collector_id']
            ]);
    }

    public function testSellerCollectorUpdateDebitDayRequired()
    {
        $data = array_merge($this->rowSellerCollector(), ["debit_day" => null]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/update', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['debit_day']
            ]);
    }

    public function testSellerCollectorUpdateWithBankIdExistRejected()
    {
        $this->seedData();
        $data = array_merge($this->rowSellerCollector(), ["bank_id" => 4]);
        $response = $this->call('POST', '/api/admin/bank-seller-collector/update/', $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['bank_id']
            ]);
    }

    public function testSellerCollectorUpdate()
    {
        $this->seedData();
        $response = $this->call('POST', '/api/admin/bank-seller-collector/update', $this->rowSellerCollector());

        $response->assertStatus(200);
        $this->assertDatabaseHas('bank_seller_collector', [
            'id' => 1,
            'bank_id' => 2,
            'seller_id' => 2,
            'collector_id' => 4,
            'close_sales_month_day' => null,
            'debit_day' => 6
        ]);

        $response = $this->call('POST', "/api/admin/bank-seller-collector/update/{}", $this->rowSellerCollector());
    }

    public function testSellerCollectorChangeStatusWithIsActiveRequerid()
    {
        $this->seedData();
        $data = array_merge($this->rowSellerCollector(), ["is_active" => null]);
        $response = $this->call('POST', "/api/admin/bank-seller-collector/{$this->rowSellerCollector()['id']}/change-status", $data);

        $response->assertStatus(422)
            ->assertJsonStructure([
                'errors' => ['is_active']
            ]);

        $response = $this->call('POST', "/api/admin/bank-seller-collector/update/{id}", $this->rowSellerCollector());
    }

    public function testSellerCollectorChangeStatus()
    {
        $this->seedData();
        $data = ["is_active" => false];
        $response = $this->call('POST', "/api/admin/bank-seller-collector/{$this->rowSellerCollector()['id']}/change-status", $data);

        $this->assertDatabaseHas('bank_seller_collector', [
            'id' => 1,
            'is_active' => false
        ]);
    }

    private function seedData()
    {
        $this->artisan('db:seed --class=BankSeeder');
        $this->artisan('db:seed --class=CompanySeeder');
        $this->artisan('db:seed --class=BankSellerCollectorSeeder');
    }

    private function rowSellerCollector()
    {
        return [
            'id' => 1,
            'bank_id' => 2,
            'seller_id' => 2,
            'collector_id' => 4,
            'close_sales_month_day' => null,
            'debit_day' => 6,
            'is_active' => false
        ];
    }
}

	
	
	
