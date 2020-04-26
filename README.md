# jsondb
A tiny JSON database in Golang

## Installation
Install using `go get github.com/Dwyane-Xu/go-jsondb`

## Usage
    import (
        "fmt"
        "encoding/json"
        "github.com/Dwyane-Xu/go-jsondb"
    )
    
    type Fish struct {
        Name   string  `json:"name"`
        Old    uint    `json:"old"`
        Weight float32 `json:"weight"`
    }
    
    func main() {
        db, err := jsondb.New("/Users/xujinzhao/许锦钊/程序/Go/go-jsondb/json-file", nil)
        if err != nil {
            fmt.Println("Error", err)
        }
    
        fish := Fish{"fish man", 3, 11.2}
        if err := db.Write("fish", "onefish", fish); err != nil {
            fmt.Println("Error", err)
        }
    
        var readFish Fish
        if err := db.Read("fish", "onefish", &readFish); err != nil {
            fmt.Println("Error", err)
        }
        fmt.Println(readFish)
    
        var fishies []Fish
        records, err := db.ReadAll("fish")
        if err != nil {
            fmt.Println("Error", err)
        }
    
        for _, f := range records {
            fishFound := Fish{}
            if err := json.Unmarshal([]byte(f), &fishFound); err != nil {
                fmt.Println("Error", err)
            }
            fishies = append(fishies, fishFound)
        }
        fmt.Println(fishies)
    
        if err := db.Delete("fish", "onefish"); err != nil {
            fmt.Println("Error", err)
        }
    
        if err := db.Delete("fish", ""); err != nil {
            fmt.Println("Error", err)
        }
    }

